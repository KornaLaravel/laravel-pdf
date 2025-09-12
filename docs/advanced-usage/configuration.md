---
title: Configuration
weight: 1
---

Laravel PDF supports configuration-based customization of Browsershot settings, allowing you to set default options that apply to all PDF generation in your application.

## Publishing the Configuration File

To publish the configuration file, run:

```bash
php artisan vendor:publish --tag=pdf-config
```

This will create a `config/laravel-pdf.php` file in your application.

## Configuration Options

The configuration file provides several sections for customizing Browsershot behavior:

### Binary Paths

Configure paths to Node.js, npm, Chrome, and other binaries:

```php
'browsershot' => [
    'node_binary' => env('LARAVEL_PDF_NODE_BINARY'),
    'npm_binary' => env('LARAVEL_PDF_NPM_BINARY'),
    'include_path' => env('LARAVEL_PDF_INCLUDE_PATH'),
    'chrome_path' => env('LARAVEL_PDF_CHROME_PATH'),
    'node_modules_path' => env('LARAVEL_PDF_NODE_MODULES_PATH'),
    'bin_path' => env('LARAVEL_PDF_BIN_PATH'),
    'temp_path' => env('LARAVEL_PDF_TEMP_PATH'),
    'write_options_to_file' => env('LARAVEL_PDF_WRITE_OPTIONS_TO_FILE', false),
    'no_sandbox' => env('LARAVEL_PDF_NO_SANDBOX', false),
],
```


## Environment Variables

You can also use environment variables to configure PDF generation:

```env
LARAVEL_PDF_NODE_BINARY=/usr/local/bin/node
LARAVEL_PDF_NPM_BINARY=/usr/local/bin/npm
LARAVEL_PDF_INCLUDE_PATH=/usr/local/bin
LARAVEL_PDF_CHROME_PATH=/usr/bin/google-chrome-stable
LARAVEL_PDF_NODE_MODULES_PATH=/path/to/node_modules
LARAVEL_PDF_BIN_PATH=/usr/local/bin
LARAVEL_PDF_TEMP_PATH=/tmp
LARAVEL_PDF_WRITE_OPTIONS_TO_FILE=true
LARAVEL_PDF_NO_SANDBOX=true
```

## Overriding Configuration

Configuration defaults can still be overridden on a per-PDF basis using the `withBrowsershot()` method:

```php
use Spatie\LaravelPdf\Facades\Pdf;
use Spatie\Browsershot\Browsershot;

// This PDF will use the configuration defaults plus the scale override
Pdf::view('invoice', ['invoice' => $invoice])
    ->withBrowsershot(function (Browsershot $browsershot) {
        $browsershot->scale(0.8);
    })
    ->save('invoice.pdf');
```

The `withBrowsershot()` closure runs after configuration defaults are applied, allowing you to modify or override any setting.

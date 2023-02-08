# lighthouse

Using the Node CLI
The Node CLI provides the most flexibility in how Lighthouse runs can be configured and reported. Users who want more advanced usage, or want to run Lighthouse in an automated fashion should use the Node CLI.

Lighthouse requires Node 16 LTS (16.x) or later.

Installation:

npm install -g lighthouse
# or use yarn:
# yarn global add lighthouse
Run it: lighthouse https://airhorner.com/

By default, Lighthouse writes the report to an HTML file. You can control the output format by passing flags.

CLI options
$ lighthouse --help

lighthouse <url> <options>

Logging:
  --verbose  Displays verbose logging  [boolean] [default: false]
  --quiet    Displays no progress, debug logs, or errors  [boolean] [default: false]

Configuration:
  --save-assets                  Save the trace contents & devtools logs to disk  [boolean] [default: false]
  --list-all-audits              Prints a list of all available audits and exits  [boolean] [default: false]
  --list-trace-categories        Prints a list of all required trace categories and exits  [boolean] [default: false]
  --additional-trace-categories  Additional categories to capture with the trace (comma-delimited).  [string]
  --config-path                  The path to the config JSON.
                                 An example config file: core/config/lr-desktop-config.js  [string]
  --preset                       Use a built-in configuration.
                                 WARNING: If the --config-path flag is provided, this preset will be ignored.  [string] [choices: "perf", "experimental", "desktop"]
  --chrome-flags                 Custom flags to pass to Chrome (space-delimited). For a full list of flags, see https://bit.ly/chrome-flags
                                 Additionally, use the CHROME_PATH environment variable to use a specific Chrome binary. Requires Chromium version 66.0 or later. If omitted, any detected Chrome Canary or Chrome stable will be used.  [string] [default: ""]
  --port                         The port to use for the debugging protocol. Use 0 for a random port  [number] [default: 0]
  --hostname                     The hostname to use for the debugging protocol.  [string] [default: "localhost"]
  --form-factor                  Determines how performance metrics are scored and if mobile-only audits are skipped. For desktop, --preset=desktop instead.  [string] [choices: "mobile", "desktop"]
  --screenEmulation              Sets screen emulation parameters. See also --preset. Use --screenEmulation.disabled to disable. Otherwise set these 4 parameters individually: --screenEmulation.mobile --screenEmulation.width=360 --screenEmulation.height=640 --screenEmulation.deviceScaleFactor=2
  --emulatedUserAgent            Sets useragent emulation  [string]
  --max-wait-for-load            The timeout (in milliseconds) to wait before the page is considered done loading and the run should continue. WARNING: Very high values can lead to large traces and instability  [number]
  --enable-error-reporting       Enables error reporting, overriding any saved preference. --no-enable-error-reporting will do the opposite. More: https://github.com/GoogleChrome/lighthouse/blob/main/docs/error-reporting.md  [boolean]
  --gather-mode, -G              Collect artifacts from a connected browser and save to disk. (Artifacts folder path may optionally be provided). If audit-mode is not also enabled, the run will quit early.
  --audit-mode, -A               Process saved artifacts from disk. (Artifacts folder path may be provided, otherwise defaults to ./latest-run/)
  --only-audits                  Only run the specified audits  [array]
  --only-categories              Only run the specified categories. Available categories: accessibility, best-practices, performance, pwa, seo  [array]
  --skip-audits                  Run everything except these audits  [array]
  --budget-path                  The path to the budget.json file for LightWallet.  [string]
  --disable-full-page-screenshot Disables collection of the full page screenshot, which can be quite large  [boolean]

Output:
  --output       Reporter for the results, supports multiple values. choices: "json", "html", "csv"  [array] [default: ["html"]]
  --output-path  The file path to output the results. Use 'stdout' to write to stdout.
                   If using JSON output, default is stdout.
                   If using HTML or CSV output, default is a file in the working directory with a name based on the test URL and date.
                   If using multiple outputs, --output-path is appended with the standard extension for each output type. "reports/my-run" -> "reports/my-run.report.html", "reports/my-run.report.json", etc.
                   Example: --output-path=./lighthouse-results.html  [string]
  --view         Open HTML report in your browser  [boolean] [default: false]

Options:
  --version                            Show version number  [boolean]
  --help                               Show help  [boolean]
  --cli-flags-path                     The path to a JSON file that contains the desired CLI flags to apply. Flags specified at the command line will still override the file-based ones.
  --locale                             The locale/language the report should be formatted in
  --blocked-url-patterns               Block any network requests to the specified URL patterns  [array]
  --disable-storage-reset              Disable clearing the browser cache and other storage APIs before a run  [boolean]
  --throttling-method                  Controls throttling method  [string] [choices: "devtools", "provided", "simulate"]
  --throttling
  --throttling.rttMs                   Controls simulated network RTT (TCP layer)
  --throttling.throughputKbps          Controls simulated network download throughput
  --throttling.requestLatencyMs        Controls emulated network RTT (HTTP layer)
  --throttling.downloadThroughputKbps  Controls emulated network download throughput
  --throttling.uploadThroughputKbps    Controls emulated network upload throughput
  --throttling.cpuSlowdownMultiplier   Controls simulated + emulated CPU throttling
  --extra-headers                      Set extra HTTP Headers to pass with request
  --precomputed-lantern-data-path      Path to the file where lantern simulation data should be read from, overwriting the lantern observed estimates for RTT and server latency.  [string]
  --lantern-data-output-path           Path to the file where lantern simulation data should be written to, can be used in a future run with the `precomputed-lantern-data-path` flag.  [string]
  --plugins                            Run the specified plugins  [array]
  --channel  [string] [default: "cli"]
  --chrome-ignore-default-flags  [boolean] [default: false]

Examples:
  lighthouse <url> --view                                                                          Opens the HTML report in a browser after the run completes
  lighthouse <url> --config-path=./myconfig.js                                                     Runs Lighthouse with your own configuration: custom audits, report generation, etc.
  lighthouse <url> --output=json --output-path=./report.json --save-assets                         Save trace, screenshots, and named JSON report.
  lighthouse <url> --screenEmulation.disabled --throttling-method=provided --no-emulatedUserAgent  Disable device emulation and all throttling
  lighthouse <url> --chrome-flags="--window-size=412,660"                                          Launch Chrome with a specific window size
  lighthouse <url> --quiet --chrome-flags="--headless"                                             Launch Headless Chrome, turn off logging
  lighthouse <url> --extra-headers "{\"Cookie\":\"monster=blue\", \"x-men\":\"wolverine\"}"        Stringify'd JSON HTTP Header key/value pairs to send in requests
  lighthouse <url> --extra-headers=./path/to/file.json                                             Path to JSON file of HTTP Header key/value pairs to send in requests
  lighthouse <url> --only-categories=performance,pwa                                               Only run the specified categories. Available categories: accessibility, best-practices, performance, pwa, seo

For more information on Lighthouse, see https://developers.google.com/web/tools/lighthouse/.
Output Examples
lighthouse
# saves `./<HOST>_<DATE>.report.html`

lighthouse --output json
# json output sent to stdout

lighthouse --output html --output-path ./report.html
# saves `./report.html`

# NOTE: specifying an output path with multiple formats ignores your specified extension for *ALL* formats
lighthouse --output json --output html --output-path ./myfile.json
# saves `./myfile.report.json` and `./myfile.report.html`

lighthouse --output json --output html
# saves `./<HOST>_<DATE>.report.json` and `./<HOST>_<DATE>.report.html`

lighthouse --output-path=~/mydir/foo.out --save-assets
# saves `~/mydir/foo.report.html`
# saves `~/mydir/foo-0.trace.json` and `~/mydir/foo-0.devtoolslog.json`

lighthouse --output-path=./report.json --output json
# saves `./report.json`
Lifecycle Examples
You can run a subset of Lighthouse's lifecycle if desired via the --gather-mode (-G) and --audit-mode (-A) CLI flags.

lighthouse http://example.com -G
# launches browser, collects artifacts, saves them to disk (in `./latest-run/`) and quits

lighthouse http://example.com -A
# skips browser interaction, loads artifacts from disk (in `./latest-run/`), runs audits on them, generates report

lighthouse http://example.com -GA
# Normal gather + audit run, but also saves collected artifacts to disk for subsequent -A runs.


# You can optionally provide a custom folder destination to -G/-A/-GA. Without a value, the default will be `$PWD/latest-run`.
lighthouse -GA=./gmailartifacts https://gmail.com
Notes on Error Reporting
The first time you run the CLI you will be prompted with a message asking you if Lighthouse can anonymously report runtime exceptions. The Lighthouse team uses this information to detect new bugs and avoid regressions. Opting out will not affect your ability to use Lighthouse in any way. Learn more.

Using the Node module
You can also use Lighthouse programmatically with the Node module.

Read Using Lighthouse programmatically for help getting started.
Read Lighthouse Configuration to learn more about the configuration options available.

Viewing a report
Lighthouse can produce a report as JSON or HTML.

HTML report:

Lighthouse example audit

Online Viewer
Running Lighthouse with the --output=json flag generates a JSON dump of the run. You can view this report online by visiting https://googlechrome.github.io/lighthouse/viewer/ and dragging the file onto the app. You can also use the "Export" button from the top of any Lighthouse HTML report and open the report in the Lighthouse Viewer.

In the Viewer, reports can be shared by clicking the share icon in the top right corner and signing in to GitHub.

Note: shared reports are stashed as a secret Gist in GitHub, under your account.

Docs & Recipes
Useful documentation, examples, and recipes to get you started.

Docs

Dealing with variance
Using Lighthouse programmatically
Testing a site with authentication
Developing Plugins
Making a New Audit
Testing on a mobile device
Setting a performance budget
Lighthouse Architecture
Recipes

Plugin - example Lighthouse plugin
Custom Audit example - extend Lighthouse, run your own audits

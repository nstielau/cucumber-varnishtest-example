# Cucumber Varnishtest Example repo

This repo is an example that uses the gem package for cucumber-varnishtest to
configure a testable VCL.  The easiest way to go would be to clone this repo
and hook into your continuous integration pipeline.

## How to use

Add the following line to your Gemfile, preferably in the test or cucumber group:

```
gem 'cucumber-varnishtest', :require => false
```

Then add the following line to your env.rb to make the step definitions available in your features:

```
require 'cucumber/varnishtest'
```

Run

```
cucumber
```

## How to use your own VCL

Simply put the .vcl file in this directory, and specify in your
`Given` clause of your Scenario:

```
Scenario: Multiple Requests without warming
  Given varnish running with MyCustomConfig.vcl <==== YOUR VCL FILE
  When we request /images.png
  Then it should pass varnishtest
```


## Dependencies

Make sure you have 'varnishtest' installed!

```
# On OSX
$ brew install varnish
$ varnishtest -h
usage: varnishtest [options] file ...
    -b size                      # Set internal buffer size (default: 512K)
    -D name=val                  # Define macro
    -i                           # Find varnishd in build tree
    -j jobs                      # Run this many tests in parallel
    -k                           # Continue on test failure
    -L                           # Always leave temporary vtc.*
    -l                           # Leave temporary vtc.* if test fails
    -n iterations                # Run tests this many times
    -q                           # Quiet mode: report only failures
    -t duration                  # Time tests out after this long
    -v                           # Verbose mode: always report test log
    -W                           # Enable the witness facility for locking
```

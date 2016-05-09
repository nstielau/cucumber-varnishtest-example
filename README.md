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

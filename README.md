
[![Build Status](https://travis-ci.org/chef/ffi-yajl.png)](https://travis-ci.org/chef/ffi-yajl)  [![Code Climate](https://codeclimate.com/github/chef/ffi-yajl.png)](https://codeclimate.com/github/chef/ffi-yajl)

# FFI YAJL

ffi-yajl is a Ruby adapter for the [yajl](http://lloyd.github.io/yajl/)
JSON parser/generator library. ffi-yajl supports multiple Ruby C
extension mechanisms, including both MRI native extensions and FFI in
order to be compatible with as many Ruby implementations as possible
while providing good performance where possible.

## Basic Usage

```ruby
require 'ffi-yajl'
json_out = FFI_Yajl::Encoder.encode( { "foo" => [ "bar", "baz" ] } )
# => "{\"foo\":[\"bar\",\"baz\"]}"
data_in = FFI_Yajl::Parser.parse( json_out )
# => {"foo"=>["bar", "baz"]}
```

## Why This Instead of X?

yajl is the only JSON library we've found that has error messages that
meet our requirements. The stdlib json gem and oj (at the time we
started this project) have error messages like "invalid token at byte
1234," which are probably fine for server use, but in
[chef](https://github.com/chef/chef) we frequently deal with
user-written JSON documents, which means we need a good user experience
when encountering malformed JSON.

We previously used brianmario's
[yajl-ruby](https://github.com/brianmario/yajl-ruby) project, but we
wanted to be able to fallback to using FFI bindings to the C code (so we
could support non-MRI rubies) and we also needed some bug fixes in
yajl2, but the maintainer wasn't able to devote enough time to the
project to make these updates in a timeframe that worked for us.

## Yajl Library Packaging

This library prefers to use the embedded yajl 2.x C library packaged in the
libyajl2 gem.  In order to use the operating system yajl library (which must be
yajl 2.x) the environment variable `USE_SYSTEM_LIBYAJL2` can be set before
installing or bundling libyajl2.  This will force the libyajl2 gem to skip
compiling its embedded library and the ffi-yajl gem will fallback to using the
system yajl library.

## Thanks

This was initially going to be a clean rewrite of an ffi ruby wrapper around
yajl2, but as it progressed more and more code was pulled in from brianmario's
existing yajl-ruby gem, particularly all the c extension code, lots of specs
and the benchmarks.  And the process of writing this would have been much more
difficult without being able to draw heavily from already solved problems in
yajl-ruby.

## License

Given that this draws heavily from the yajl-ruby sources, and could be
considered a derivative work, the MIT License from that project has been
preserved and this source code has deliberately not been dual licensed under
Chef's typical Apache License.  See the
[LICENSE](https://github.com/chef/ffi-yajl/blob/master/LICENSE) file in this
project.


# Faraday::Tracer

OpenTracing compatible Faraday middleware.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'faraday-tracer'
```

## Usage

```ruby
require 'opentracing'
OpenTracing.global_tracer = TracerImplementation.new

require 'faraday'
require 'faraday/tracer'

# Use already existing span to use it as as a parent span. In case there is no
# existing span leave it nil to start a new trace.
span = request.env['rack.span'] # when using rack-tracer gem

conn = Faraday.new(url: 'http://localhost:3000/') do |faraday|
  faraday.use Faraday::Tracer, span: span

  # default Faraday stack
  faraday.request :url_encoded
  faraday.adapter Faraday.default_adapter
end
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/salemove/faraday-tracer.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).


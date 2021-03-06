# Nbs

Simple wrapper for the [NextBigSound](https://www.nextbigsound.com) [api](https://api3.nextbigsound.com)

Requires key and granted access from NextBigSound

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'nbs'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install nbs

## Usage

Set config variables, at the moment all that is needed is access key:

`Nbs.setup "your_access_key"`

In a config file eg (rails)

>config/initializers/nbs.rb

### Artist search

Nbs.artist_search("a tribe called quest")

results in
```
[
    [0] {
                     :id => "7440",
                   :name => "A Tribe Called Quest",
        :music_brainz_id => "9689aa5a-4471-4fb4-9721-07cecda0fa9f"
    },
    [1] {
                     :id => "80756",
                   :name => "De La Soul feat. A Tribe Called Quest",
        :music_brainz_id => nil
    },
    [2] {
                     :id => "66202",
                   :name => "A Tribe Called Quest, Aphrodite, Groove Armada & The Chi-Lites",
        :music_brainz_id => nil
    }
]
```

### Metrics and Profiles
instance based on nbs id
```
default_options = {
  from: 7 days ago (epoch time),
  to: now (epoch time)
}
nbs = Nbs.new(7440, default_options)
```

`nbs.metrics[:facebook]` returns

```
[
    [0] {
          :time => 2017-05-30 00:00:00 UTC,
        :volume => 1589996
    },
    [1] {
          :time => 2017-05-31 00:00:00 UTC,
        :volume => 1590014
    },
    [2] {
          :time => 2017-06-01 00:00:00 UTC,
        :volume => 1590044
    },
    [3] {
          :time => 2017-06-02 00:00:00 UTC,
        :volume => 1589990
    },
    [4] {
          :time => 2017-06-03 00:00:00 UTC,
        :volume => 1589967
    },
    [5] {
          :time => 2017-06-04 00:00:00 UTC,
        :volume => 1589941
    },
    [6] {
          :time => 2017-06-05 00:00:00 UTC,
        :volume => 1589968
    }
]
```

available metrics via gem (more available through api)

>*facebook, instagram, twitter, youtube*

Typically results go as far back as 3 months

`nbs.artist_profiles` returns

```
[
    [0] {
        :nbs_profle_id => "9946716",
                  :url => "http://www.facebook.com/therealrunthejewels"
    },
    [1] {
        :nbs_profle_id => "9946718",
                  :url => "http://twitter.com/runjewels"
    },
    [2] {
        :nbs_profle_id => "9946719",
                  :url => "http://www.youtube.com/channel/UCeveumRTn2o--9j1Xz2KUCQ"
    },
    [3] {
        :nbs_profle_id => "16209803",
                  :url => "http://instagram.com/runthejewels"
    }
]
```

### Metric
```
Nbs.metric('9946716', {})
default_options = { start: (Time.now - 3.day).to_i,
                    end: Time.now.to_i,
                    metric: 'fans' }
```
returns metrics for a single profile. eg:
```
[
    [0] {
          :time => 2017-07-09 00:00:00 UTC,
        :volume => 64608
    },
    [1] {
          :time => 2017-07-10 00:00:00 UTC,
        :volume => 64737
    },
    [2] {
          :time => 2017-07-11 00:00:00 UTC,
        :volume => 64903
    }
]
```


## Development

After checking out the repo, run `bin/setup` to install dependencies. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/eicore/nbs.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

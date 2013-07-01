#!/usr/bin/env ruby
#^syntax detection
################################################################################
# RUBYGEM DEVELOPMENT PATTERN
#
# This pattern allows easy development of dependent RubyGems without having to
# resort to any crazy "magic".
#
# To use this pattern, define the gem you wish to develop with using the
# 'gem_dev' method instead of the usual 'gem' method.  Then clone said gems
# source under the 'vender/checkouts' directory of this repository.
#
# Once you have these two items complete; you can then declare "GEMDEV=1" via
# your environment and this will cause the Gemfile to switch the gem source
# from the standard RubyGems/private repositories to using a ':path' option
# pointing to the source under 'vendor/checkouts' which will cause bundler to
# use your local copy of the gem allowing you to perform changes on the gems
# source in real-time.
#
# Additionally if you want the 'Gemfile' to be verbose and let you know what
# it's doing you can declare "VERBOSE=1" in your environment.
#
# Under normal circumstances the 'Gemfile' and 'gem_dev' methods will function
# as if you had defined the gems using the 'gem' method.
################################################################################
def gem_dev(gem_name, *args)
  verbose = (ENV['VERBOSE'] == "1")
  gemdev = (ENV['GEMDEV'] == "1")

  if (File.exists?(path = File.join("vendor", "checkouts", gem_name)) && gemdev)
    if (arg = args.first{ |arg| arg.is_a?(Hash) })
      arg.reject!{ |k,v| [:git,:ref].include?(k) }
      arg.merge!(:path => path)
    else
      args << {:path => path}
    end
  end

  if verbose
    gem_details = args.collect{ |arg| arg.inspect }.join(", ")
    !gem_details.empty? and (gem_details = ", #{gem_details}")
    puts("%2sGEMDEV: %32s%s" % [((gemdev == true) ? "  " : "NO"), gem_name, gem_details])
  end

  gem(gem_name, *args)
end
################################################################################

source "https://rubygems.org"

gem_dev "testlab"
gem_dev "lxc"
gem_dev "ztk"

gem "pry"

gem "activesupport", "< 4.0.0" if (RUBY_VERSION < "1.9.3")
gem "json" if (RUBY_VERSION == "1.8.7")

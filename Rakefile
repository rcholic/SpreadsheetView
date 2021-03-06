require 'xcjobs'

namespace :test do
  desc 'test on simulator'
  task :iphonesimulator do |t, args|
    XCJobs::Test.new("simulator") do |t|
      configuration = ENV['CONFIGURATION']
      destination = ENV['DESTINATION']
      testcase = ENV['TESTCASE']
      configuration = 'Debug' if configuration.empty?
      
      t.workspace = 'SpreadsheetView'
      t.scheme = 'SpreadsheetView'
      t.sdk = 'iphonesimulator'
      t.configuration = configuration
      t.add_only_testing("SpreadsheetViewTests/#{testcase}") unless testcase.empty?
      t.add_destination(destination) unless destination.empty?
      t.add_build_option('-enableCodeCoverage', 'YES')
      t.add_build_setting('ONLY_ACTIVE_ARCH', 'YES')
      t.add_build_setting('ENABLE_TESTABILITY', 'YES') if configuration == 'Release'
      t.build_dir = 'build'
    end
    Rake::Task['simulator'].execute
  end

  desc 'test on device'
  task :iphoneos do |t, args|
    XCJobs::Test.new("device") do |t|
      t.workspace = 'SpreadsheetView'
      t.scheme = 'SpreadsheetView'
      t.sdk = 'iphoneos'
      configuration = args['configuration'] || 'Debug'
      t.configuration = configuration
      if configuration == 'Release'
        t.add_build_setting('ENABLE_TESTABILITY', 'YES')
      end
      t.build_dir = 'build'
    end
    Rake::Task['device'].execute
  end
end

XCJobs::Coverage::Coveralls.new()

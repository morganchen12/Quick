def run(command)
  system(command) or raise "RAKE TASK FAILED: #{command}"
end

namespace "test" do
  desc "Run unit tests for all iOS targets"
  task :ios do |t|
    run "xcodebuild -workspace Quick.xcworkspace -scheme Quick-iOS -destination 'platform=iOS Simulator,name=iPhone 6' clean test"
  end

  desc "Run unit tests for all OS X targets"
  task :osx do |t|
    run "xcodebuild -workspace Quick.xcworkspace -scheme Quick-OSX clean test"
  end

  desc "Run unit tests for all iOS and OS X targets using xctool"
  task xctool: %w[test:xctool:ios test:xctool:osx]
  namespace :xctool do
    desc "Run unit tests for all iOS targets using xctool"
    task :ios do |t|
      run "xctool -workspace Quick.xcworkspace -scheme Quick-iOS -sdk iphonesimulator -destination 'platform=iOS Simulator,name=iPhone 6' clean test"
    end

    desc "Run unit tests for all OS X targets using xctool"
    task :osx do |t|
      run "xctool -workspace Quick.xcworkspace -scheme Quick-OSX clean test"
    end
  end
end

namespace "templates" do
  install_dir = File.expand_path("~/Library/Developer/Xcode/Templates/File Templates/Quick")
  src_dir = File.expand_path("../Quick Templates", __FILE__)

  desc "Install Quick templates"
  task :install do
    if File.exists? install_dir
      raise "RAKE TASK FAILED: Quick templates are already installed at #{install_dir}"
    else
      mkdir_p install_dir
      cp_r src_dir, install_dir
    end
  end

  desc "Uninstall Quick templates"
  task :uninstall do
    rm_rf install_dir
  end
end

task default: ["test:ios", "test:osx"]


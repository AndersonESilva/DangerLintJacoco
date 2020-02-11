# Sometimes it's a README fix, or something like that - which isn't relevant for
# including in a project's CHANGELOG for example
declared_trivial = github.pr_title.include? "#trivial"

# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn("PR is classed as Work in Progress") if github.pr_title.include? "[WIP]"

# Warn when there is a big PR
warn("Big PR") if git.lines_of_code > 500

# Don't let testing shortcuts get into master by accident
fail("fdescribe left in tests") if `grep -r fdescribe specs/ `.length > 1
fail("fit left in tests") if `grep -r fit specs/ `.length > 1

# Android Lint
begin
  android_lint.skip_gradle_task = true
  android_lint.report_file = "app/build/reports/lint-results-developDebug.xml"
  android_lint.lint
rescue => ex
  failure("Deu ruim no LINT: #{ex}")
end

# Jacoco
begin
  jacoco.minimum_project_coverage_percentage = 5 # default 0
  jacoco.minimum_class_coverage_percentage = 50 # default 0
  jacoco.report("app/build/reports/jacoco/jacocoTestReport/jacocoTestReport.xml")
rescue => ex
  failure("Deu ruim no JaCoCo (verificacao da Cobertura): #{ex}")
end

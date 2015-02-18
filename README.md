## The issue

`rake db:test:prepare` is run before individual tests.

## Replicating the issue

```sh
$ git clone https://github.com/notalex/rails_sample_app
$ cd rails_sample_app
$ git checkout test_issue
$ bundle install
$ ruby -I test test/models/user_test.rb
```

Since there is no table for users, the test completes within a second. To verify if `rake db:test:prepare` is indeed run, one will have to watch the ps output while the test is running.

```sh
$ watch -n 0.5 'ps aux | grep db:test:prepare | grep -v grep'
```

For real projects involving some amount of tables, this individual test run would take more time. This issue is not seen in the previous rails version(4.1.7).

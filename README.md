# RecipientInterceptor

[![Build Status](https://secure.travis-ci.org/croaky/recipient_interceptor.png)](http://travis-ci.org/croaky/recipient_interceptor?branch=master)

Never accidentally send emails to real people from your staging environment.

## Rails example

Send all staging emails to a group email address without accidentally emailing
users with active email addresses in the database.

In `Gemfile`:

```ruby
gem 'recipient_interceptor'
```

In `config/environments/staging.rb`:

```ruby
Mail.register_interceptor RecipientInterceptor.new(ENV['EMAIL_RECIPIENTS'])
```

From the command line:

```ruby
heroku config:add EMAIL_RECIPIENTS="staging@example.com" --remote staging
```

## Options

Optionally prefix the subject line:

```ruby
Mail.register_interceptor(
  RecipientInterceptor.new(
    ENV['EMAIL_RECIPIENTS'],
    subject_prefix: '[STAGING]',
  ),
)
```

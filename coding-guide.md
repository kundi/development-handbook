# Ruby

### Code Style

For keeping our Ruby code in shape we use [Rubocop](https://github.com/rubocop-hq/rubocop), which is a static code analyzer and formatter based on Ruby community best practices.

Every Ruby (on Rails) project needs to pass Rubocop check to create a valid build. When developing, Rubocop is able to correct misstyled code with `rubocop -a` command in the app root folder.

It is mandatory to make the Rubocop check pass before you push any code.

#### Documenting methods

Non-trivial Ruby methods need to be documented in developer friendly way. The preferred way of documenting is [YARD](https://yardoc.org/).

A good example:

```
class SendApproachingBillingRemindersJob
  include Sidekiq::Worker

  ## Performs the job of querying for paying accounts that will be billed
  #  in `next_billing_in` days and sends their owners an email informing them about
  #  the upcoming billing.
  #
  # @param next_billing_in [ActiveSupport::Duration] specifies a period to find
  # accounts that are about to be billed in given period from now. Default: 1.week
  # @param plan_period [Integer] specifies which plans do the queried accounts need to
  # belong to; monthly or yearly. Possible options: 30, 365. Default: 365.
  # @return [Array<Account>] the accounts whose owners have been emailed
  def perform(next_billing_in = 1.week, plan_period = 365)
    ...
  end
end
```

#### Use of parenthesis with function calls

Always use parenthesis when calling functions or methods, except in DSL.

```
things = filter_things(things) # Good
things = filter_things things  # Bad
..

after_create :do_something # Good
```

### Testing

For testing we use [RSpec](https://relishapp.com/rspec/rspec-rails/v/3-0/docs/directory-structure). Before pushing code, make sure the tests succeed: run `rspec` in the app's root folder.

# JavaScript

### Code Style

It is mandatory to use the modern (ES6+) style of JavaScript. If you run into a CoffeeScript file and you need to do changes to it, the rule is to convert it to JavaScript with [decaffeinate](https://decaffeinate-project.org).

It is mandatory to use [Prettier](https://github.com/prettier/prettier) code formatter. It enforces a consistent style by parsing code on the fly, so install it in your code editor or IDE.

### Testing

In Ember projects, use the internal testing framework.

# CSS

Use [BEM](http://getbem.com/).

# Git

It is mandatory to always treat master branch as a production stable branch.

When something needs merging into master, push the code into a branch and create a pull request to master (or another branch).

### Naming conventions for branches

Use a prefix with a branch top-level description (bugfix, feature, improvement, miscellaneous). Examples:

```
bugfix/stop-input-flickering
feature/retention-graph
improvement/query-performance
misc/proxies-experiment
```

### How to write commit messages

- Capitalize sentences, use proper grammar,
- Prefix the message with the module name the code affects,
- When more detailed explanation is needed (this is always welcome), separate the subject with a blank line and write the details.

**Important**: refer to the [Commit Message Guidelines
](https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53).

### Examples of good commit messages:

![good commit message 1](https://i.imgur.com/O1hObSb.png)

![good commit message 2](https://i.imgur.com/LPtBHCB.png)

### Examples of bad commit messages:

![bad commit message 1](https://i.imgur.com/rv7AzGA.png)

![bad commit message 2](https://i.imgur.com/lfwqTWY.png)

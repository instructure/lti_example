LTI Outcome Service Example
---------------------------

## Instructure Canvas

This is a simple example of writing an LTI tool provider that utilizes
the outcome service support in Canvas to post a grade back to Canvas
when the user finishes using the tool. Rather than presenting a real
assessment, this tool will just present the user with an HTML form text
field where they can enter their desired score.

The tool is written in Ruby using the Sinatra web framework and the
OAuth gem. You'll need to have ruby installed, with rubygems.

### Running the Tool

To run this tool, download the git repository, then open a console
prompt in the repo directory.

First, if you don't already have Bundler installed, do that.

    $ gem install bundler

You may need to run this command as root depending on your ruby
configuration.

Next you'll want to install the necessary gems:

    $ bundle install

Now, just start it up:

    $ ruby -rubygems lti_example.rb

You will see some output like this:

    Sinatra/1.3.1 has taken the stage on 4567 for development with backup from WEBrick

That number is the port that the tool is running on (4567 is the default).

### Configuring Canvas

Next, you'll need to configure a course in Canvas to point to your
now-running LTI tool. The first step is to add the tool to the course
settings, external tools tab. The consumer key is "test", the secret is
"secret". The URL will likely be
"http://localhost:4567/assessment/start", though the hostname and port
may change if you are not running the tool on the same computer as your
web browser.

Here is what your configuration should look like:

![tool config](/codekitchen/lti_outcomes_example/raw/master/tool_config.png)

Now that the tool is configured, you'll need to set up an Assignment
that points to the tool. This step is what lets you define how many
points the tool is worth, and links the tool into the course gradebook
in Canvas.

On the Assignments tab in the same course, create a new assignment of
type "External Tool". Click the "more options" link, and you'll see a
dialog asking you which tool to use:

![assignment config](/codekitchen/lti_outcomes_example/raw/master/assignment_config.png)

Select your newly-configured tool and save the assignment. Now when you
go to the assignment page as a student, the tool will launch, and you
can take the external tool assessment! Once you've stepped through the
assessment, you can look at the grades tab in Canvas and verify that the
grade from the tool was saved into Canvas.

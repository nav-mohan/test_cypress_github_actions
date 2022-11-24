<h1> Example Github Actions to run Cypress Tests </h1>

```

name: End-to-end tests
on:
  pull_request:
    branches:
      - "master"
jobs:
  cypress-run: # this is the name of this job. this is what Github Status Checks refers to
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      # Install NPM dependencies, cache them correctly
      # and run all Cypress tests
      - name: Cypress run
        uses: cypress-io/github-action@v4

```
<li>
The template GHAction <code>cypress-io/github-action@v4</code> installs all the NPM dependencies and runs the tests automatically. 
</li>
<li> The job is called "<code>cypress-run</code>" <b>(line 7)</b>. This is the name used by Github for doing <a href = "https://help.github.com/en/github/administering-a-repository/enabling-required-status-checks">status checks</a> </li>
<li> To protect the <code>master</code> branch with a status check 
  <ul> <code>Settings</code> --> <code>Branches</code> --> <code>Add Rule </code></ul>
  <ul> Use <code>"master"</code> for the <code>Branch name pattern</code></ul>
  <ul>Check the option <code> Require status checks to pass before merging </code></ul>
  <ul> In the search bar, type in the name of the job. Which in this case was "<code>cypress-run</code>". Its not "<code>End-to-end tests</code>"!
</li>
<li> Now when a <code>pull-request</code> is made to the <code>master</code> branch, it first runs through these Cypress tests. If the tests fail, the merge is not completed.
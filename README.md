
<!---
Documentation generated by Skydoc
-->
<h1>Python pex rules for Bazel</h1>


<nav class="toc">
  <h2>Rules</h2>
  <ul>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#pex_pytest">pex_pytest</a></li>
    <li><a href="#pex_repositories">pex_repositories</a></li>
    <li><a href="#pex_binary">pex_binary</a></li>
    <li><a href="#pex_library">pex_library</a></li>
    <li><a href="#pex_test">pex_test</a></li>
  </ul>
</nav>
<hr>

<a name="overview"></a>
## Overview

[![Build Status](https://travis-ci.org/benley/bazel_rules_pex.svg?branch=master)](https://travis-ci.org/benley/bazel_rules_pex)

### Setup

Add something like this to your WORKSPACE file:

    git_repository(
        name = "io_bazel_rules_pex",
        remote = "https://github.com/benley/bazel_rules_pex.git",
        tag = "0.2.2",
    )
    load("@io_bazel_rules_pex//pex:pex_rules.bzl", "pex_repositories")
    pex_repositories()

In a BUILD file where you want to use these rules, or in your
`tools/build_rules/prelude_bazel` file if you want them present repo-wide, add:

    load(
        "@io_bazel_rules_pex//pex:pex_rules.bzl",
        "pex_binary",
        "pex_library",
        "pex_test",
        "pex_pytest",
    )

Lastly, make sure that `tools/build_rules/BUILD` exists, even if it is empty,
so that Bazel can find your `prelude_bazel` file.

<a name="pex_pytest"></a>
## pex_pytest

<pre>
pex_pytest(<a href="#pex_pytest.name">name</a>, <a href="#pex_pytest.srcs">srcs</a>, <a href="#pex_pytest.deps">deps</a>, <a href="#pex_pytest.eggs">eggs</a>, <a href="#pex_pytest.data">data</a>, <a href="#pex_pytest.args">args</a>, <a href="#pex_pytest.flaky">flaky</a>, <a href="#pex_pytest.local">local</a>, <a href="#pex_pytest.size">size</a>, <a href="#pex_pytest.timeout">timeout</a>)
</pre>

A variant of pex_test that uses py.test to run one or more sets of tests.

This produces two things:

  1. A pex_binary (`<name>_runner`) containing all your code and its
     dependencies, plus py.test, and the entrypoint set to the py.test
     runner.
  2. A small shell script to launch the `<name>_runner` executable with each
     of the `srcs` enumerated as commandline arguments.  This is the actual
     test entrypoint for bazel.

Almost all of the attributes that can be used with pex_test work identically
here, including those not specifically mentioned in this docstring.
Exceptions are `main` and `entrypoint`, which cannot be used with this macro.


<a name="pex_pytest_args"></a>
### Attributes


<table class="params-table">
  <colgroup>
    <col class="col-param" />
    <col class="col-description" />
  </colgroup>
  <tbody>
    <tr id="pex_pytest.name">
      <td><code>name</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#name">Name</a>; Required</code></p>
        <p>A unique name for this rule.</p>
      </td>
    </tr>
    <tr id="pex_pytest.srcs">
      <td><code>srcs</code></td>
      <td>
        <p><code>Unknown; Required</code></p>
        <p>List of files containing tests that should be run.</p>
      </td>
    </tr>
    <tr id="pex_pytest.deps">
      <td><code>deps</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_pytest.eggs">
      <td><code>eggs</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_pytest.data">
      <td><code>data</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_pytest.args">
      <td><code>args</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_pytest.flaky">
      <td><code>flaky</code></td>
      <td>
        <p><code>Unknown; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_pytest.local">
      <td><code>local</code></td>
      <td>
        <p><code>Unknown; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_pytest.size">
      <td><code>size</code></td>
      <td>
        <p><code>Unknown; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_pytest.timeout">
      <td><code>timeout</code></td>
      <td>
        <p><code>Unknown; Optional</code></p>
        
      </td>
    </tr>
  </tbody>
</table>
<a name="pex_repositories"></a>
## pex_repositories

<pre>
pex_repositories()
</pre>

Rules to be invoked from WORKSPACE for remote dependencies.

<a name="pex_binary"></a>
## pex_binary

<pre>
pex_binary(<a href="#pex_binary.name">name</a>, <a href="#pex_binary.deps">deps</a>, <a href="#pex_binary.data">data</a>, <a href="#pex_binary.srcs">srcs</a>, <a href="#pex_binary.eggs">eggs</a>, <a href="#pex_binary.entrypoint">entrypoint</a>, <a href="#pex_binary.interpreter">interpreter</a>, <a href="#pex_binary.main">main</a>, <a href="#pex_binary.pex_use_wheels">pex_use_wheels</a>, <a href="#pex_binary.pex_verbosity">pex_verbosity</a>, <a href="#pex_binary.reqs">reqs</a>, <a href="#pex_binary.zip_safe">zip_safe</a>)
</pre>

Build a deployable pex executable.


<a name="pex_binary_args"></a>
### Attributes


<table class="params-table">
  <colgroup>
    <col class="col-param" />
    <col class="col-description" />
  </colgroup>
  <tbody>
    <tr id="pex_binary.name">
      <td><code>name</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#name">Name</a>; Required</code></p>
        <p>A unique name for this rule.</p>
      </td>
    </tr>
    <tr id="pex_binary.deps">
      <td><code>deps</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>Python module dependencies.</p>
<p><code>pex_library</code> and <code>py_library</code> rules should work here.</p>
      </td>
    </tr>
    <tr id="pex_binary.data">
      <td><code>data</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>Files to include as resources in the final pex binary.</p>
<p>Putting other rules here will cause the <em>outputs</em> of those rules to be
embedded in this one. Files will be included as-is. Paths in the archive
will be relative to the workspace root.</p>
      </td>
    </tr>
    <tr id="pex_binary.srcs">
      <td><code>srcs</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_binary.eggs">
      <td><code>eggs</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p><code>.egg</code> and <code>.whl</code> files to include as python packages.</p>
      </td>
    </tr>
    <tr id="pex_binary.entrypoint">
      <td><code>entrypoint</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>Name of a python module to use as the entrypoint.</p>
<p>e.g. <code>your.project.main</code></p>
<p>If unspecified, the <code>main</code> attribute will be used.
It is an error to specify both main and entrypoint.</p>
      </td>
    </tr>
    <tr id="pex_binary.interpreter">
      <td><code>interpreter</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>Path to the python interpreter the pex should to use in its shebang line.</p>
      </td>
    </tr>
    <tr id="pex_binary.main">
      <td><code>main</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>File to use as the entrypoint.</p>
<p>If unspecified, the first file from the <code>srcs</code> attribute will be used.</p>
      </td>
    </tr>
    <tr id="pex_binary.pex_use_wheels">
      <td><code>pex_use_wheels</code></td>
      <td>
        <p><code>Boolean; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_binary.pex_verbosity">
      <td><code>pex_verbosity</code></td>
      <td>
        <p><code>Integer; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_binary.reqs">
      <td><code>reqs</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        <p>External requirements to retrieve from pypi, in <code>requirements.txt</code> format.</p>
<p>This feature will reduce build determinism!  It tells pex to resolve all
the transitive python dependencies and fetch them from pypi.</p>
<p>It is recommended that you use <code>eggs</code> instead where possible.</p>
      </td>
    </tr>
    <tr id="pex_binary.zip_safe">
      <td><code>zip_safe</code></td>
      <td>
        <p><code>Boolean; Optional</code></p>
        
      </td>
    </tr>
  </tbody>
</table>
<a name="pex_library"></a>
## pex_library

<pre>
pex_library(<a href="#pex_library.name">name</a>, <a href="#pex_library.deps">deps</a>, <a href="#pex_library.data">data</a>, <a href="#pex_library.srcs">srcs</a>, <a href="#pex_library.eggs">eggs</a>, <a href="#pex_library.reqs">reqs</a>)
</pre>




<a name="pex_library_args"></a>
### Attributes


<table class="params-table">
  <colgroup>
    <col class="col-param" />
    <col class="col-description" />
  </colgroup>
  <tbody>
    <tr id="pex_library.name">
      <td><code>name</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#name">Name</a>; Required</code></p>
        <p>A unique name for this rule.</p>
      </td>
    </tr>
    <tr id="pex_library.deps">
      <td><code>deps</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>Python module dependencies.</p>
<p><code>pex_library</code> and <code>py_library</code> rules should work here.</p>
      </td>
    </tr>
    <tr id="pex_library.data">
      <td><code>data</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>Files to include as resources in the final pex binary.</p>
<p>Putting other rules here will cause the <em>outputs</em> of those rules to be
embedded in this one. Files will be included as-is. Paths in the archive
will be relative to the workspace root.</p>
      </td>
    </tr>
    <tr id="pex_library.srcs">
      <td><code>srcs</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_library.eggs">
      <td><code>eggs</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p><code>.egg</code> and <code>.whl</code> files to include as python packages.</p>
      </td>
    </tr>
    <tr id="pex_library.reqs">
      <td><code>reqs</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        <p>External requirements to retrieve from pypi, in <code>requirements.txt</code> format.</p>
<p>This feature will reduce build determinism!  It tells pex to resolve all
the transitive python dependencies and fetch them from pypi.</p>
<p>It is recommended that you use <code>eggs</code> instead where possible.</p>
      </td>
    </tr>
  </tbody>
</table>
<a name="pex_test"></a>
## pex_test

<pre>
pex_test(<a href="#pex_test.name">name</a>, <a href="#pex_test.deps">deps</a>, <a href="#pex_test.data">data</a>, <a href="#pex_test.srcs">srcs</a>, <a href="#pex_test.eggs">eggs</a>, <a href="#pex_test.entrypoint">entrypoint</a>, <a href="#pex_test.interpreter">interpreter</a>, <a href="#pex_test.main">main</a>, <a href="#pex_test.pex_use_wheels">pex_use_wheels</a>, <a href="#pex_test.pex_verbosity">pex_verbosity</a>, <a href="#pex_test.reqs">reqs</a>, <a href="#pex_test.zip_safe">zip_safe</a>)
</pre>




<a name="pex_test_args"></a>
### Attributes


<table class="params-table">
  <colgroup>
    <col class="col-param" />
    <col class="col-description" />
  </colgroup>
  <tbody>
    <tr id="pex_test.name">
      <td><code>name</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#name">Name</a>; Required</code></p>
        <p>A unique name for this rule.</p>
      </td>
    </tr>
    <tr id="pex_test.deps">
      <td><code>deps</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>Python module dependencies.</p>
<p><code>pex_library</code> and <code>py_library</code> rules should work here.</p>
      </td>
    </tr>
    <tr id="pex_test.data">
      <td><code>data</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p>Files to include as resources in the final pex binary.</p>
<p>Putting other rules here will cause the <em>outputs</em> of those rules to be
embedded in this one. Files will be included as-is. Paths in the archive
will be relative to the workspace root.</p>
      </td>
    </tr>
    <tr id="pex_test.srcs">
      <td><code>srcs</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_test.eggs">
      <td><code>eggs</code></td>
      <td>
        <p><code>List of <a href="http://bazel.io/docs/build-ref.html#labels">labels</a>; Optional</code></p>
        <p><code>.egg</code> and <code>.whl</code> files to include as python packages.</p>
      </td>
    </tr>
    <tr id="pex_test.entrypoint">
      <td><code>entrypoint</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>Name of a python module to use as the entrypoint.</p>
<p>e.g. <code>your.project.main</code></p>
<p>If unspecified, the <code>main</code> attribute will be used.
It is an error to specify both main and entrypoint.</p>
      </td>
    </tr>
    <tr id="pex_test.interpreter">
      <td><code>interpreter</code></td>
      <td>
        <p><code>String; Optional</code></p>
        <p>Path to the python interpreter the pex should to use in its shebang line.</p>
      </td>
    </tr>
    <tr id="pex_test.main">
      <td><code>main</code></td>
      <td>
        <p><code><a href="http://bazel.io/docs/build-ref.html#labels">Label</a>; Optional</code></p>
        <p>File to use as the entrypoint.</p>
<p>If unspecified, the first file from the <code>srcs</code> attribute will be used.</p>
      </td>
    </tr>
    <tr id="pex_test.pex_use_wheels">
      <td><code>pex_use_wheels</code></td>
      <td>
        <p><code>Boolean; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_test.pex_verbosity">
      <td><code>pex_verbosity</code></td>
      <td>
        <p><code>Integer; Optional</code></p>
        
      </td>
    </tr>
    <tr id="pex_test.reqs">
      <td><code>reqs</code></td>
      <td>
        <p><code>List of strings; Optional</code></p>
        <p>External requirements to retrieve from pypi, in <code>requirements.txt</code> format.</p>
<p>This feature will reduce build determinism!  It tells pex to resolve all
the transitive python dependencies and fetch them from pypi.</p>
<p>It is recommended that you use <code>eggs</code> instead where possible.</p>
      </td>
    </tr>
    <tr id="pex_test.zip_safe">
      <td><code>zip_safe</code></td>
      <td>
        <p><code>Boolean; Optional</code></p>
        
      </td>
    </tr>
  </tbody>
</table>

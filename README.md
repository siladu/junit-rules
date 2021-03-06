junit-rules
===========

[![Build Status](https://travis-ci.org/unruly/junit-rules.svg?branch=master)](https://travis-ci.org/unruly/junit-rules)

A collection of useful JUnit rules from Unruly's codebases

## Install from Maven Central

```xml
<dependency>
    <groupId>co.unruly</groupId>
    <artifactId>junit-rules</artifactId>
    <version>1.0</version>
</dependency>
```

## Ignore tests until a certain date or datetime.

This allows you to write an acceptance/integration test before implementing a feature, and integrate it into your codebase before the implementation is complete.

```java
@Rule
IgnoreUntilRule rule = new IgnoreUntilRule();

@IgnoreUntil("2014-10-30")
@Test
public void example_test_ignored_until_a_date() {

}

@IgnoreUntil("2014-10-30T17:30:00")
@Test
public void example_test_ignored_until_a_datetime() {

}
```

## Quarantine non-deterministic tests

```java
@Rule QuarantineRule rule = new QuarantineRule();

@NonDeterministic(retries=3)
public void some_sporadically_failing_test() {

}
```

QuarantineRule supports a functional interface called QuarantineRuleLogger as a constructor argument for additional logging capabilities. For example, we email ourselves failures so it's harder to ignore.

```java
@Rule QuarantineRule rule = new QuarantineRule(msg -> System.err.println(msg));
```

## Make sure tests pass reliably

We use this to diagnose tests as being non-deterministic. To run each test 10 times:

```java
@Rule ReliabilityRule rule = new ReliabilityRule(10);
```

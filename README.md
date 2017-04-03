# rheactor-event-store

[![Build Status](https://travis-ci.org/ResourcefulHumans/rheactor-event-store.svg?branch=master)](https://travis-ci.org/ResourcefulHumans/rheactor-event-store)
[![monitored by greenkeeper.io](https://img.shields.io/badge/greenkeeper.io-monitored-brightgreen.svg)](http://greenkeeper.io/) 
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)
[![semantic-release](https://img.shields.io/badge/semver-semantic%20release-e10079.svg)](https://github.com/semantic-release/semantic-release)
[![Test Coverage](https://codeclimate.com/github/ResourcefulHumans/rheactor-event-store/badges/coverage.svg)](https://codeclimate.com/github/ResourcefulHumans/rheactor-event-store/coverage)
[![Code Climate](https://codeclimate.com/github/ResourcefulHumans/rheactor-event-store/badges/gpa.svg)](https://codeclimate.com/github/ResourcefulHumans/rheactor-event-store)

[![NPM](https://nodei.co/npm/rheactor-event-store.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/rheactor-event-store/)

Implementation of an event store based on [redis](https://redis.io/).

Contains [helper methods to manage secondary indices](https://github.com/ResourcefulHumans/rheactor-event-store/blob/master/src/aggregate-index.js).

## Mutable Aggregates have been deprecated

The initial implementation of the event store modified models in place. More recently we decied to use immutable models instead. 

The [`ImmutableAggregateRepository`](https://github.com/ResourcefulHumans/rheactor-event-store/blob/master/src/immutable-aggregate-repository.js) changes how Models are instantiated. It moves the responsibility of creating the model instance to the repository, where the `applyEvent()` method is invoked as a reducer. The method will return an instance of [`ImmutableAggregateRoot`](https://github.com/ResourcefulHumans/rheactor-event-store/blob/master/src/immutable-aggregate-root.js) which can no longer be manipulated directly.

This also changes how meta information is stored in the Aggregates, it is now encapsuled in a separate object called [`AggregateMeta`](https://github.com/ResourcefulHumans/rheactor-event-store/blob/master/src/aggregate-meta.js).

See the [tests](https://github.com/ResourcefulHumans/rheactor-event-store/blob/master/test/immutable-aggregate-repository.spec.js) for details.


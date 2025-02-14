---
author: Elliot Forbes
date: 2019-11-24T11:05:52Z
desc: In this Challenge, you will be improving the HTTP server you originally developed in the second Go Challenge!
image: golang.png
draft: true
weight: 3
series:
  - go-challenges
tags:
  - go
title: Challenge 03 - Improving your HTTP Server in Go
twitter: https://twitter.com/Elliot_F
language: go
---

> This challenge will be to split up the new REST API application you have developed in Challenge 2 and utilize Go Modules. 

# Challenge

Go Modules and the go mod tool have been deemed the official strategy for managing dependencies in your Go applications. Break up the existing application so that you create an entry point main.go file in the root of your directory as well as a sub-module which contains your endpoint code.

## Acceptance Criteria

In order to successfully complete this challenge, your project will have to:

* Use Go Modules as a means of managing your dependencies
* Contain a `main.go` file which references a module `stats` which is contained within a `stats/stats.go` file within your project. This `stats/stats.go` file must contain the logic for collecting the hardware utilization stats from your machine and exposing them as a HTTP function. 

# Key Concepts

* You will learn how to effectively break up your simple Go applications into larger, better structured applications using Go Modules as your dependency management system

# Completing the Challenge

In order to complete the challenge, fork the [elliotforbes/go-challenges](https://github.com/elliotforbes/go-challenges) repository into your own GitHub account. 

Next, create a directory within that repo for each of the challenges you attempt! This will give you a super handy repo that will contain excellent references for your own future Go projects!

## Helpful Tutorials
  
The following tutorials should help you to complete this challenge:

* [Go Modules Tutorial](https://tutorialedge.net/golang/go-modules-tutorial/)

# Conclusion

Congratulations! You have successfully completed the 3rd TutorialEdge Go Challenge!
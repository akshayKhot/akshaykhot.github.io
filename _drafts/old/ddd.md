---
layout: post
title: Domain-Driven Design
---



[Chapter 1. Domain Model](/domain-model)

[Chapter 2. Ubiquitous Language](/domain-language)

The model is a set of concepts built up in the heads of people on the project, with terms and relationships that reflect domain insight. To create a good design, you need a shared team language. 

Domain experts have limited understanding of the technical jargon of software development, but they use the jargon of their field. Developers, on the other hand, may create abstractions that support their design but are not understood by the domain experts. 

<a target="_blank" href="{{ site.images }}/{{ page.img }}">
  <img src="{{ site.images }}/{{ page.img }}" alt="">
</a>  Diagram

The domain experts vaguely describe what they want. Developers, struggling to understand a domain new to them, vaguely understand. 

On a project without a common language, developers have to translate for domain experts. Domain experts translate between developers and still other domain experts. Developers even translate for each other. Translation muddles model concepts, **a project faces serious problems when its language is fractured.**

The domain model can provide a common language that a project needs. The domain language allows developers and domain experts to communicate with each other, and for the domain experts to communicate among themselves about requirements, development planning, and features. The more pervasively the language is used, the more smoothly understanding will flow.
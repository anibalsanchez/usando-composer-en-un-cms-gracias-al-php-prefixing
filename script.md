# Using Composer in a CMS

Welcome, everybody, it's a delight to be here in the Joomlashack conference, presenting "Using Composer in a CMS".

## About me

My name is Aníbal Sánchez. It's a great opportunity be here sharing with you our experiences managing successful projects and developing extensions for Joomla.

I've been the Extly's team leader for about 10 years, and I'm the co-founder of the PHP-Prefixer, a service that we have recently launched in November.

It's been a fascinating service to create, and we are excited to start sharing what can be done combining Joomla and Composer technologies.

## A volunteer

As a Joomla volunteer, I've been collaborating with the project for more than 5 years. At this time, I'm completing my second term as the Extensions Directory (JED) Team Leader; and I can say that it has been an immense pleasure contributing to the community.

If you are interested in Joomla and you want to contribute, I invite you to join the project. Joomla is always looking for new volunteers, and contributing is the way to help the project.

## Perfect Publisher

To present a profile about what I do, I'm going to introduce 3 of our projects. The first one is "Perfect Publisher".

Perfect Publisher is an extension to share content from Joomla to social networks.

Since all social networks have libraries to integrate their APIs, this project has been our very first early encounter with PHP libraries.

At this time, the extension has more than +30 Social Media Integrations and implements more than +60 Composer Libraries.

It has been an enormous challenge to pack the libraries and publish them during 8 years of development.

In this session, I'll be presenting several points of what we have done for Perfect Publisher.

## XT Search for Algolia

XT Search is one of our recent projects, where we integrated the Algolia search technology with Joomla AND PrestaShop.

We took the official Algolia library, designed the business library to create the index of different types of content, and deployed the solution on Joomla and PrestaShop.

This project has been our success case to prove that the solution can be developed with Composer several platforms at the same time.

## SI San Juan

Finally, since not everything is extensions or packages that can be distributed on open source platforms,

I present the SI San Juan project, a project where we work as tech consultants, running Joomla on a High Availability Cluster,

In this particular case, we've created a distributed case solution based on Redis managed via a Laravel Channel.

All these initiates are perfect examples of what can be achieved leveraging technology that it is available as Composer libraries and Joomla.

## Prerequisites

This presentation is going to be about PHP development and specifically about the development of solutions for Joomla using Composer.

I'm going to do my best to be clear,

explaining why it is an absolute necessity to use Composer in the development of business solutions.

On the other hand, many topics are in the area of advanced PHP, so feel free to send me questions or feedback if something is not clear enough.

## What is Composer?

Five years ago, I was working on an extension, and I had a problem.

The Library was available in Packagist; I could manually download it and package it in the extension. Most of the time, the components and modules could use the Library perfectly fine.

However, I ran into a situation where I needed to use a library, but, other developers were also using the same Library but a different version that it was incompatible with my requirements.

There were collisions (naming conflicts or differences in the functions between versions)

This problem was an invitation to start exploring what Composer is, the classic use cases where it shines, the limitations and the solutions that we can apply.

For starters, with the dependency manager, you declare in a project definition what libraries you require to use, and Composer downloads the libraries.

Additionally, Composer manages the libraries versions and dependencies between libraries.

Composer design is heavily influenced by other successful projects such as Node.js's "npm" and Ruby's "bundler".

For four and a half years ago, I've been investigating Composer and how it works, and different solutions to the original problem.

My objectives of today's talk are to share with you those learnings and cover the fundamental ways that Composer provides to manage libraries, and how it can be used on a Joomla solution.

I'm going to share with you some tips and tricks that I've learned to help save you some of the pain.

And discuss an innovative service that we have invented to overcome Composer architectural limitations.

## Packagist

Side by side with Composer, we have Packagist. The main site where you can search for libraries, and know every detail about the requirement and the popularity of the published packages.

## Motivation of Composer Usage

In the slides, I have written this phrase about "standing on the shoulders of Giants" to represent the idea that our achievements are always based on the works of others.

Composer helps us as developers to integrate the fantastic works that other people create, that we don't be hesitant to incorporate libraries from successful projects, and I encourage you to look for new answers with Composer.

## More reasons

1. **Adopt the most recent PHP innovations**: One of the aspects that always surprises me is that you can always find someone who is an early adopter of the latest PHP news. It has already tested and published an early version of a library.

For instance, now we can say that PHP 8 is available as a stable version, but there is also a Symfony Polyfill to support PHP8 since February.

2. Once you have a good grasp on Composer and how you can associate libraries and different domains, you can start to creating at different scales.

Choosing frameworks or libraries according to different needs and trusting on components that are already developed and proven.

3. Also, if we want to develop with other frameworks, other practices or for different platforms, we have to establish a domain that is neutral to the underlying platforms.

For instance: if we develop an invoice system, we want to be focused on the business aspects and be free to port the domain to the systems that we need.

4. 5. 6. The additional benefits of Library Management are that we can define libraries of knowledge, improving how we define or domain or the semantic of our systems

The main incentive is focusing on the software definition and in the business rules of the domain, instead of having to solve everything.

## Classic extension

In a classic extension, we define Components, Modules, Plugins, Libraries and a Command-Line; and all these assets use the Joomla framework similarly.

## A modern solution centered on a library

When we change our mind, and we start to think in Composer terms, everything is in the Library.

I'm saying that the Library that the extension installs has all our domain source code and all the associated Composer libraries.

The Composer Libraries packaged in our Library and delimited, and they are naturally developed and tested separately.

Following this definition, the Componentes, Modules, etc are entry points. The user interface. And, we can separate them from the Library.

At the same time, we can also clearly define the calls from the Library to the CMS Framework.

## Composer in Joomla terms

At the Joomla core, Joomla is already including Composer Libraries.

These libraries are installed in the `library/vendor`.

The Composer schema defines what libraries are installed.

In this case, it installs the part of the Joomla Framework that it is available on Composer and some other libraries.

The obvious question is if we can change the Composer schema of Joomla core. The answer is No; only the product team can change this part of Joomla.

## The extensions can use Composer

Of course, we are almost totally free to use Composer libraries in our extensions.

## Composer as an "utility"

The first way of using Composer is replacing the usage of the Joomla classic autoloader.

The autoloader is the mechanism that helps PHP to discover where the source code can be found in files.

Using Composer, we can declare a single autoloaded, and it will automagically load the source code that follows the definitions.

## FIG PSR-4 Standard

The PSR-4 standard is the definition of the class names, files and folders that allow Composer to autoload the source code of the project.

## PSR-4 Example

This is a case from an extension, that defines where the code of the package is located and where the automated tests are located.

The idea is not packing the code for development and generating the final version of the autoloader only with the production code.

## Classmap & Autoloading

Composer also supports the most basic case of autoloading classes and files, where we can declare a folder or the files to be autoloaded.

## Generated maps

Internally, what Composer does is generating maps associating the classes and files that have to loaded dynamically.

## Everything in the Library

Again, according to our practice separating the Library, packing most of the code in a library is the best way to distribute a package.

This is the tree of a ZIP file of one of our extensions.

## The Laravel Starter

To present these ideas, I have created this starter project for Joomla.

In the starter project, we have the main project with the general definition of the package.

The package depends on a library that internally defines the usage of Laravel and Tailwind CSS.

## The Laravel Starter - The View

The Library has a simple view to render a list of 10 articles.

## Where is the catch

Until now, the architecture is sound, Composer is great, and there are thousands of PHP developers using it. So, it looks like it works perfectly fine.

However, there is one catch.

Composer works perfectly as a standalone dependency manager, designed to work only on the developer computer.

It is not designed to work online on a site.

And, it is a tool to be used at the development time.

If we plan to use Composer libraries in an extension, other techniques must be used to solve the potential problems.

To exemplify the potential issue, we have two separate teams of developers using the same libraries.

If they can coordinate the project definitions, then it can work fine.

But, if they don't have standard definitions, then the problem in the use of libraries can appear.

## Where is the catch - Example

For instance, in the starter project, we have these library definitions.

In particular, the project is using the Guzzle library v7.

## Where is the catch - Two teams

If we have another team using version 5 of Guzzle,

installing the package and

executing the extension at the same time, then conflicts can appear.

## Where is the catch - A conflict

For instace, this is how an asynchronic request is sent in Guzzle v7 and this is how it was done in v5.

So, to avoid these differences, something has to be done to prevent them.

## Prefixing PHP

The most common way to solve the Composer conflicts between teams is prefixing PHP.

Changing the source code to add a prefix where the conflicts can appear.

For instance, this is a piece of code from the Carbon Datetime library.

## Prefixing PHP - Case 1

This is how we added "Extly" to the namespace to identify the Library in our extensions uniquely.

There are many cases to prefix, but the general idea is the same.

Add a prefix to uniquely identify objects.


## The first Real-world Case

The first case that I remember that I found that uses this technique is Akeeba's FOF.

In this case, FOF uses Pimple as the container, and the class has the FOF to define the proper context.


## Can we prefix entire projects?

In our work, after start using Composer, and having to prefix entire libraries, we started to wonder how we could automate the manual task of prefixing.

We started with a few commands to search and replace following specific rules.

After a while, our first solution evolved in a full package, based on a rule engine to do static analysis of PHP and generate the source code at the project level.

So, the answer to the question was: Yes, we can prefix entire projects, and the results are astounding.

## Introducing PHP Prefixer

That's how we arrived at the idea of creating a full online service to offer the PHP prefixing as a service.

The prefixing service is a computing-intensive task.

The prefixing engine has to parse all files, analyse the dependencies of all libraries and perform several phases. So, it runs on hardware on multi-core instances, powered with a fair amount of memory.

We have launched the service barely a month ago, and we are still developing the SaaS service, but it is already available.

We didn't want to miss the opportunity to present it here. So, here it is.

## Let's prefix an extension 1

So, how it works the prefixing service.

Revising the starter project.

## Let's prefix an extension 2

The composer schema has an extra configuration that defines the prefix.

## Prefixing PHP - Create

So, we can upload the Library to the service.

## Prefixing PHP - Download

And, after a few minutes, the service generates the output file.

## Prefixing PHP - Testing

The output files can be tested in the same way than the original libraries.

And, the resulting Library must perform precisely in the same way than the original libraries.

## Prefixing PHP - Results

As a glimpse of what is done, this is the automated output of the service.

In this file, we can check how the file from the Carbon library it has been prefixed in the same than a manual prefix would be applied.

## Conclusion

In this short presentation, I've synthetised the rationale behind the usage of Composer, why it is vital for the development of an extension, and I think that the evolution of PHP is currently linked to Composer as the dependency manager.

I presented the case to use Composer in a standalone model and in the case of publicly distributing a prefixed extension.

I know that using Composer implies the redesign of the software to be oriented to the usage of libraries.

Still, the potential benefits outweigh the initial learning process and the work to transform the packages.

There's a lot of cognitive load when you embrace Composer as the package manager.

The main challenge is thinking in terms of packages and libraries.

The benefit is straightforward, using the whole database of PHP Libraries and improving the management of our business domain.

## Questions - Feedback


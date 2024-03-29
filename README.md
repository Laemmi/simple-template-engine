[![Build Status](https://travis-ci.org/Laemmi/simple-template-engine.svg?branch=master)](https://travis-ci.org/Laemmi/simple-template-engine)
[![Latest Stable Version](https://poser.pugx.org/laemmi/simple-template-engine/v/stable)](https://packagist.org/packages/laemmi/simple-template-engine)
[![Total Downloads](https://poser.pugx.org/laemmi/simple-template-engine/downloads)](https://packagist.org/packages/laemmi/simple-template-engine)
[![Latest Unstable Version](https://poser.pugx.org/laemmi/simple-template-engine/v/unstable)](https://packagist.org/packages/laemmi/simple-template-engine)
[![License](https://poser.pugx.org/laemmi/simple-template-engine/license)](https://packagist.org/packages/laemmi/simple-template-engine)

# Simple template engine
This is very simple template engine to parse templates.

## Requirements
php 7.2

## Installation

via composer

    composer require laemmi/simple-template-engine

or use repository

    git clone https://github.com/Laemmi/simple-template-engine.git
    
## Usage
In this package you have to compiler. Once for replacing variable and one for if statements.
For the variable compiler you can use modifiers. In default you can use all php functions like strtoupper etc.

### Use with factory

    $template = TemplateFactory::factory('My name is {if $name}{#name|strtoupper#}{/if} and i am {#age#} years old.');
    $template->name = 'Michael';
    $template->age  = 99;
    $template();
    
    // My name is MICHAEL and i am 99 years old.
    
### Use with callback modifier 

    $callback = new ModifierCallback('custom', function($value) {
        return sprintf('Sir %s', $value);
    });

    $compiler = new CompileVariable();
    $compiler->addModifier($callback);

    $template = new Template('My name is {#name|custom#}');
    $template->addPlugin($compiler);
    $template->name = 'Michael';
    $template();
    
    // My name is Sir Michael

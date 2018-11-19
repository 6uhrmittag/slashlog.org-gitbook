# Changelog Template

## 15.0.0 - 2042-12-03

### Fixed

* Removed humans, they weren't doing fine with animals.

### Changed

* Animals are now super cute, all of them.

## 14.0.0 - 2042-10-06

### Added

* Introduced animals into the world, we believe they're going to be a neat addition.


# callouts

> #### primary::Title
>
> text

- 

> #### success::Title
>
> text

-

> #### danger::Title
>
> text

-

> #### warning::Title
>
> text

-

> #### info::Title
>
> text

-


# codetabs

This is a code block with tabs for each languages:

{% codetabs name="Python", type="py" -%}
msg = "Hello World"
print msg
{%- language name="JavaScript", type="js" -%}
var msg = "Hello World";
console.log(msg);
{%- language name="HTML", type="html" -%}
<b>Hello World</b>
{%- endcodetabs %}

# quiz

<quiz name="Gitbook Quiz">
    <question multiple>
        <p>What is gitbook used for?</p>
        <answer correct>To read books</answer>
        <answer>To book hotel named git</answer>
        <answer correct>To write and publish beautiful books</answer>
        <explanation>GitBook.com lets you write, publish and manage your books online as a service.</explanation>
    </question>
    <question>
        <p>Is it quiz?</p>
        <answer correct>Yes</answer>
        <answer>No</answer>
    </question>
    <question>
        <p>This is multiple dropdown quiz, in each dropdown select a correct number corresponding to the dropdown's order</p>
        <answer>
            <option correct>First</option>
            <option>Second</option>
            <option>Third</option>
            <option>Fourth</option>
        </answer>
        <answer>
            <option>First</option>
            <option correct>Second</option>
            <option>Third</option>
            <option>Fourth</option>
        </answer>
        <answer>
            <option>First</option>
            <option>Second</option>
            <option correct>Third</option>
            <option>Fourth</option>
        </answer>
        <answer>
            <option>First</option>
            <option>Second</option>
            <option>Third</option>
            <option correct>Fourth</option>
        </answer>
    </question>
</quiz>


# api

{% method %}
## Install {#install}

The first thing is to get the GitBook API client.

{% sample lang="shell" %}
```bash
$ npm install gitbook-api
```

{% endmethod %}


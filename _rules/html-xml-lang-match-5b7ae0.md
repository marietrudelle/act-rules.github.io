---
id: 5b7ae0
name: HTML lang and xml:lang match
rule_type: atomic
description: |
  The rule checks that for the `html` element, there is no mismatch between the primary language in non-empty `lang` and `xml:lang` attributes, if both are used.
accessibility_requirements:
  wcag20:3.1.1: # Language of Page (A)
    forConformance: true
    failed: not satisfied
    passed: further testing needed
    inapplicable: further testing needed
input_aspects:
  - DOM Tree # The tree that HTML is parsed into.
authors:
  - Annika Nietzio
  - Jey Nandakumar
---

## Applicability

The root element of the page, if it is an `html` element with both `lang` and `xml:lang` attributes that has a [valid language subtag](#valid-language-subtag).

## Expectation

The value of the primary language subtag (characters before the first dash) for the `lang` and `xml:lang` attributes are the same.

**Note**: HTML 5 specification requires the `lang` and `xml:lang` attributes to match exactly. This is not known to impact accessibility, which is why it is permitted in this rule.

## Assumptions

- Although there is no known way that an inappropriate secondary subtag in the `lang` or `xml:lang` attribute (such as "en-XYZ") can lead to accessibility issues, it is conceivable that with specific assistive technologies on some languages, there can be exceptions. In that case `lang` and `xml:lang` should have matching secondary subtags.

## Accessibility Support

Since most assistive technologies will consistently use `lang` over `xml:lang` when both are used, violation of this rule may not necessarily be a violation of WCAG 2. Only when there are inconsistencies between assistive technologies, as to which attribute is used to determine the language, does this lead to a violation of SC 3.1.1.

## Background

- [https://www.w3.org/TR/2014/NOTE-WCAG20-TECHS-20140408/H57](https://www.w3.org/TR/2014/NOTE-WCAG20-TECHS-20140408/H57)
- [https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang)
- [https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/xml:lang](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/xml:lang)
- [https://www.w3.org/TR/WCAG20-TECHS/H57.html](https://www.w3.org/TR/WCAG20-TECHS/H57.html)

## Test Cases

### Passed

#### Passed Example 1

`html` element with matching value for `lang` and `xml:lang`.

```html
<html lang="en" xml:lang="en"></html>
```

#### Passed Example 2

`html` element with varied case but matching value for `lang` and `xml:lang`.

```html
<html lang="en" xml:lang="En"></html>
```

#### Passed Example 3

`html` element with varied case but matching primary sub-tag value for `lang` and `xml:lang`.

```html
<html lang="en" xml:lang="en-GB"></html>
```

#### Passed Example 4

`html` element with varied case but matching primary sub-tag value for `lang` and `xml:lang`.

```html
<html lang="en-GB" xml:lang="en"></html>
```

#### Passed Example 5

`html` element with varied case but matching primary sub-tag value for `lang` and `xml:lang`, albeit the value `XYZ` is not valid.

```html
<html lang="en-XYZ" xml:lang="en"></html>
```

### Failed

#### Failed Example 1

`html` element with non-matching value for `lang` and `xml:lang`.

```html
<html lang="fr" xml:lang="en"></html>
```

### Inapplicable

#### Inapplicable Example 1

`svg` element is not applicable for this rule.

```svg
<svg xmlns="http://www.w3.org/2000/svg" lang="en" xml:lang="en">
```

#### Inapplicable Example 2

`xml:lang` is empty, the rule mandates `non-empty` values.

```html
<html lang="fr" xml:lang=""></html>
```

#### Inapplicable Example 3

Only `non-empty` values are considered.

```html
<html lang="" xml:lang=""></html>
```

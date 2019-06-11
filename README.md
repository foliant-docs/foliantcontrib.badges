![](https://img.shields.io/pypi/v/foliantcontrib.badges.svg)

# Badges

Preprocessor for Foliant which helps to add badges to your documents. It uses [Shields.io](https://shields.io) to generate badges.

# Installation

```bash
$ pip install foliantcontrib.badges
```

# Config

To enable the preprocessor, add `badges` to `preprocessors` section in the project config:

```yaml
preprocessors:
    - badges
```

The preprocessor has a number of options:

```yaml
preprocessors:
    - badges:
        server: 'https://img.shields.io'
        as_object: true
        add_link: true
        vars:
            jira_path: localhost:3000/jira
            package: foliant
```

`server`
:    Shields server URL, which hosts badges. default: `https://img.shields.io`

`as_object`
:    If `true` — preprocessor inserts `svg` badges with HTML `<object>` tag, instead of Markdown image tag (`![]()`). This is required for links and hints to work. default: `true`

`add_link`
:    If `true` preprocessor tries to determine the link which should be added to badge (for example, link to jira issue page for jira issue badge). Only works with `as_object = true`. default: `true`

> Please note that right now only links for **pypi** and **jira-issue** badges are being added automatically. Please contribute or contact author for adding other services.

`vars`
:    Dictionary with variables which will be replaced in badge urls. See **variables** section.

# Usage

Just add the `badge` tag and specify path to badge in the tag body:

```
<badge>jira/issue/https/issues.apache.org/jira/kafka-2896.svg</badge>
```

## Variables

You can use variables in your badges to replace parts which repeat often. For example, if we need to add many badges to our Jira tracker, we may put the protocol and host parameters into a variable like this:

```yaml
preprocessors:
    - badges:
        vars:
            jira: https/issues.apache.org/jira
```

To reference a variable in a badge path use syntax `${variable}`:

```
<badge>jira/issue/${jira}/kafka-2896.svg</badge>

Description of the issue goes here. But it's not the only one.

<badge>jira/issue/${jira}/KAFKA-7951.svg</badge>

Description of the second issue.
```

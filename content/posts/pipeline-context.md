---
title: "Sharing dynamic state in GitHub workflow"
date: 2022-12-23T18:43:50Z
draft: false
tags: ['github', 'ci/cd']
categories : ['Development']
---

It is common to define and use dynamic variables in GitHub actions. Typical use cases are labelling docker images or generating artifact names. This note outlines the steps required to achieve the goal.

## The key points to remember

* The step that shares a value must have the property `id` set to be referenced by the rest of the steps
* It is possible to print the context, and it makes it easier to troubleshoot

```yaml
jobs:
  # Build job
  build:
    # ...
    steps:
        - name: share a {key, value} pair 
          id: some_step_id
          run: echo "some_key=some_value" >> $GITHUB_OUTPUT
        
        - name: [debugging] dump the context
          run: echo '${{ toJSON(steps) }}'
        
        - name: use the {key, value} pair
          run: echo "the value = ${{ steps.some_step_id.outputs.some_key }}" 
```

## Troubleshooting

Dumping the value in JSON format makes troubleshooting an easy task. The line 11 the snippet above will produce the following data. 

```yaml
{
...
  ,
  "some_step_id": {
    "outputs": {
      "some_key": "some_value"
    },
    "outcome": "success",
    "conclusion": "success"
  },
 }
```

## References

[Setting an output parameter](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#setting-an-output-parameter)


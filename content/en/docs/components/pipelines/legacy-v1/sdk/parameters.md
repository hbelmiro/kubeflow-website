+++
title = "Pipeline Parameters"
description = "Passing data between pipeline components"
weight = 70
                    
+++
{{% alert title="Old Version" color="warning" %}}
This page is about __Kubeflow Pipelines V1__, please see the [V2 documentation](/docs/components/pipelines) for the latest information.

Note, while the V2 backend is able to run pipelines submitted by the V1 SDK, we strongly recommend [migrating to the V2 SDK](/docs/components/pipelines/user-guides/migration).
For reference, the final release of the V1 SDK was [`kfp==1.8.22`](https://pypi.org/project/kfp/1.8.22/), and its reference documentation is [available here](https://kubeflow-pipelines.readthedocs.io/en/1.8.22/).
{{% /alert %}}

The [`kfp.dsl.PipelineParam` 
class](https://kubeflow-pipelines.readthedocs.io/en/stable/source/dsl.html#kfp.dsl.PipelineParam)
represents a reference to future data that will be passed to the pipeline or produced by a task.

Your pipeline function should have parameters, so that they can later be configured in the Kubeflow Pipelines UI.

When your pipeline function is called, each function argument will be a `PipelineParam` object.
You can pass those objects to the components as arguments to instantiate them and create tasks.
A `PipelineParam` can also represent an intermediate value that you pass between pipeline tasks.
Each task has outputs and you can get references to them from the `task.outputs[<output_name>]` dictionary.
The task output references can again be passed to other components as arguments.

In most cases you do not need to construct `PipelineParam` objects manually.

The following code sample shows how to define a pipeline with parameters:

```python
@kfp.dsl.pipeline(
  name='My pipeline',
  description='My machine learning pipeline'
)
def my_pipeline(
    my_num: int = 1000, 
    my_name: str = 'some text', 
    my_url: str = 'http://example.com'
):
  ...
  # In the pipeline function body you can use the `my_num`, `my_name`, 
  # `my_url` arguments as PipelineParam objects.
```

For more information, you can refer to the guide on
[building components and pipelines](/docs/components/pipelines/legacy-v1/sdk/component-development/).
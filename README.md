# Deep dive Tekton

A `task` is an activity that can be reused and defines a series of steps that deliver the task's functionality. A `clustertask` is a task that has the scope of an entire cluster. It is composed of the following main properties:
 - `steps`: The list of `steps` that will implement the task's behavior.
 - `params`: (Optional) Parameters that can be used to modify certain values in a `task.`
 - `workspaces`: (Optional) The list of workspaces. Use `workspaces` to store files generated by steps in a `task`.
 - `results`: (Optional) Can be used to store small values as pod's termination messages.
 - `stepTemplate`: (Optional) Can be used to define default values for `steps` in this file.

A `taskrun` is a definition of how a `task` should execute in a cluster and it follows the `task` up to the completion of the defined `steps`. It is composed of the following main properties:
 - `taskRef`: has the name of the task that needs to be execute.
 - `status`: This field is updated whenever the `taskrun` finishes its execution.
 - `podTemplate`: (Optional) Specifies the contents of the pod template that will be used as the basis for the `task` pod. The full list of supported fields can be found [here](https://github.com/tektoncd/pipeline/blob/master/docs/podtemplates.md).

A `pipeline` is a series of tasks that provides the workflow to deliver or deploy an artifact. It is comprised of the following main properties:
 - `spec`: Specifies the configuration information for this Pipeline object. This must include:
   - `tasks`: Specifies the Tasks that composed the Pipeline and the details of their execution.
 - `task`
   - `resources.inputs` / `resources.output`
     - `from`: Indicates the data for a `PipelineResource` originates from the output of a previous `Task`.
   - `runAfter`: Indicates that a `Task` should execute after one or more other `Tasks` without output linking.
   - `retries`: Specifies the number of times to retry the execution of a `Task` after a failure. Does not apply to execution cancellations.
   - `conditions`: Specifies Conditions that only allow a `Task` to execute if they evaluate to `true`.
   - `timeout`: Specifies the timeout before a `Task` fails.
 - `results`: Specifies the location to which the `Pipeline` emits its execution results.
 - `description`: Holds an informative description of the `Pipeline` object.

A `pipelinerun` is a definition of how a `pipeline` should execute in a cluster and it follows up to the completion of the defined `tasks`. It is composed of the following main properties:
 - 

## Tasks Tutorial

### 00 - Echo

Take a look at how to generate a `task`. Verify how easy it is to create a new `task`.

```shell
$ k apply -f 00-echo
```

### 01 - Workspaces

```shell
$ kubectl apply -f 01-workspaces
```

### 02 - Results

```shell
$ kubectl apply -f 02-results
```

### 03 - StepTemplate

```shell
$ kubectl apply -f 03-step-template
```

## Pipelines Tutorial

### 10 - Simple Pipeline

```shell
$ kubectl apply -f 10-simple-pipeline
```

### 11 - Triggers

```shell
$ kubectl apply -f 11-triggers
```

### 12 - complex pipeline

```shell
$ kubectl apply -f 12-complex-pipeline
```
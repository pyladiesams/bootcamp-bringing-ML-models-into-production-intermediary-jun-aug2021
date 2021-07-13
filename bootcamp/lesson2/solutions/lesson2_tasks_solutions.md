# Bringing ML Models into Production Bootcamp
# Lesson 2: Batch Inference

## Solutions to exercise 1: Register ML model
### Steps

1. Register the same model via cli
```
az ml model register \
--name linear_regression \
--model-framework ScikitLearn \
-p <your local path to the model> \
-g mlops_bootcamp \
-w mlops
```
2. Register the same model via Python script by using Model.register method
```
from azureml.core import Model, Workspace
ws = Workspace.from_config()

model = Model.register(model_path="linear_regression.pkl",
        model_name="linear_regression",
        model_framework=Model.Framework.SCIKITLEARN,
        workspace=ws)
```

3. (Optional) Register the same model via Python script by using run.register method
```
from azureml.core import Run
<define and create run here>
model = run.register_model(model_name="linear_regression",
        model_path="outputs/linear_regression.pkl"
        model_framework="ScikitLearn")
```
---
## Solutions to exercise 2: Attach and remove inference cluster

### Steps

1. Attach an inference cluster via Python script
```
from azureml.core import Workspace
from azureml.core.compute import ComputeTarget, AmlCompute
from azureml.core.compute_target import ComputeTargetException

ws = Workspace.from_config()

# Choose a name for your CPU cluster
cpu_cluster_name = "cpucluster"

# Verify that cluster does not exist already
try:
    cpu_cluster = ComputeTarget(workspace=ws, name=cpu_cluster_name)
    print('Found existing cluster, use it.')
except ComputeTargetException:
    # To use a different region for the compute, add a location='<region>' parameter
    compute_config = AmlCompute.provisioning_configuration(vm_size='STANDARD_D2_V2',
                                                           max_nodes=4)
    cpu_cluster = ComputeTarget.create(ws, cpu_cluster_name, compute_config)

cpu_cluster.wait_for_completion(show_output=True)
```
2. Remove this inference cluster via CLI
```
az ml computetarget delete \
> --name cpucluster \
> -g mlops_bootcamp \
> -w mlops
```
3. Optional (Remove this inference cluster via Python script)
```
from azureml.core import Workspace
from azureml.core.compute import ComputeTarget

ws = Workspace.from_config()

# cluster name to remove
cpu_cluster_name = "cpucluster"

cpu_cluster = ComputeTarget(workspace=ws, name=cpu_cluster_name)
cpu_cluster.delete()
```
---
## Solutions to exercise 3: Schedule Azure Machine Learning pipeline

### Steps

1. Schedule the pipeline to run every Wednesday at 08:00 in the morning via Python Script
```



ws = Workspace.from_config()
<retieve the id of the published pipeline and assign it to pipeline_id>

weekly_wed_morning = ScheduleRecurrence(frequency='Week', interval=1,
                                        week_days="Wednesday", time_of_day="08:00")
pipeline_schedule = Schedule.create(ws, name='Weekly Morning Predictions',
                                        description='batch inferencing',
                                        pipeline_id=<the ID of the pipeline the schedule will submit - str>,
                                        experiment_name='Batch_Prediction',
                                        recurrence=weekly_wed_morning)
```
2. Schedule the pipeline to run every day at 13:00 via Python Script
```
from azureml.core import Workspace
from azureml.pipeline.core import ScheduleRecurrence, Schedule
ws = Workspace.from_config()

<retieve the id of the published pipeline and assign it to pipeline_id>

daily = ScheduleRecurrence(frequency='Day', interval=1, time_of_day="13:00")
pipeline_schedule = Schedule.create(ws, name='Daily Noon Predictions',
                                        description='batch inferencing',
                                        pipeline_id=<the ID of the pipeline the schedule will submit - str>,
                                        experiment_name='Batch_Prediction',
                                        recurrence=daily)
```
3. Deactivate the scheduled pipeline via Python Script
```
from azureml.core import Workspace
from azureml.pipeline.core import Pipeline, PublishedPipeline
from azureml.pipeline.core import Schedule

ws = Workspace.from_config()

# If the pipeline is scheduled, you must cancel the schedule first.
# Retrieve the schedule's identifier from the portal or by running:

ss = Schedule.list(ws)
for s in ss:
    print(s)

# Once you have the schedule_id you wish to disable, run:

def stop_by_schedule_id(ws, schedule_id):
    s = next(s for s in Schedule.list(ws) if s.id == schedule_id)
    s.disable()
    return s

stop_by_schedule_id(ws, schedule_id)
```
4. Optional (Explore other possible steps in the pipeline)

Explore [steps Package](https://docs.microsoft.com/en-us/python/api/azureml-pipeline-steps/azureml.pipeline.steps?view=azure-ml-py) that contains pre-built steps that can be executed in an Azure Machine Learning Pipeline.

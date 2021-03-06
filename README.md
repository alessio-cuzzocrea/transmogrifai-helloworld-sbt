# TransmogrifAI Hello World for SBT

First, [Download Spark 2.4.5](https://spark.apache.org/downloads.html)

### Define SPARK_HOME environment variable
```
export SPARK_HOME=your_spark_home_dir
```

### Run TitanicSimple:

```
./sbt "sparkSubmit \
    --class com.salesforce.hw.OpTitanicSimple \
    -- $PWD/src/main/resources/TitanicDataset/TitanicPassengersTrainData.csv"
```

## Titanic model

### Train
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.titanic.OpTitanic -- \
    --run-type=train --model-location=/tmp/titanic-model \
    --read-location Passenger=$PWD/src/main/resources/TitanicDataset/TitanicPassengersTrainData.csv"
```

### Score
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.titanic.OpTitanic -- \
    --run-type=score --model-location=/tmp/titanic-model \
    --read-location Passenger=$PWD/src/main/resources/TitanicDataset/TitanicPassengersTrainData.csv \
    --write-location /tmp/titanic-scores"
```

### Evaluate
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.titanic.OpTitanic -- \
    --run-type evaluate \
    --model-location /tmp/titanic-model \
    --read-location Passenger=$PWD/src/main/resources/TitanicDataset/TitanicPassengersTrainData.csv \
    --write-location /tmp/titanic-eval \
    --metrics-location /tmp/titanic-metrics"
```

## Boston house model

### Train
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.boston.OpBoston -- \
    --run-type=train --model-location=/tmp/boston-model \
    --read-location BostonHouse=$PWD/src/main/resources/BostonDataset/housing.data"
```

### Score
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.boston.OpBoston -- \
    --run-type=score --model-location=/tmp/boston-model \
    --read-location BostonHouse=$PWD/src/main/resources/BostonDataset/housing.data \
    --write-location /tmp/boston-scores"
```

### Evaluate
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.boston.OpBoston -- \
    --run-type evaluate \
    --model-location /tmp/boston-model \
    --read-location BostonHouse=$PWD/src/main/resources/BostonDataset/housing.data \
    --write-location /tmp/boston-eval \
    --metrics-location /tmp/boston-metrics"
```

## Iris model

### Train
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.iris.OpIris -- \
    --run-type=train --model-location=/tmp/iris-model \
    --read-location Iris=$PWD/src/main/resources/IrisDataset/iris.data"
```

### Score
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.iris.OpIris -- \
    --run-type=score --model-location=/tmp/iris-model \
    --read-location Iris=$PWD/src/main/resources/IrisDataset/bezdekIris.data \
    --write-location /tmp/iris-scores"
```

### Evaluate
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.iris.OpIris -- \
    --run-type evaluate \
    --model-location /tmp/iris-model \
    --read-location Iris=$PWD/src/main/resources/IrisDataset/bezdekIris.data \
    --write-location /tmp/iris-eval \
    --metrics-location /tmp/iris-metrics"
```

## Data Preparation
```
./sbt "sparkSubmit \
    --class com.salesforce.hw.dataprep.JoinsAndAggregates -- \
    $PWD/src/main/resources/EmailDataset/Clicks.csv \
    $PWD/src/main/resources/EmailDataset/Sends.csv"

./sbt "sparkSubmit \
    --class com.salesforce.hw.dataprep.ConditionalAggregation -- \
    $PWD/src/main/resources/WebVisitsDataset/WebVisits.csv"
```

## Verify the Results

Look for the output file(s) in the location you specified. For instance, you can use `avro-tools` to inspect the scores files (on mac simply run `brew install avro-tools` to install it).

Other than that, the best way to verify the results is to look through the logs that should have been generated during the run. It has all kinds of information about the features the processing and the model reliability.

## Generate your own workflow

Experiment with adding feature changes or exploring more models in any of the provided workflows.

See how high you can get your auROC!

# PySpark Architecture

This repository contains my understanding and practice of **PySpark architecture** and how a Spark application works in a cluster environment.

## PySpark Architecture Diagram

![PySpark Architecture](Pyspark%20Architecture.png)

## How PySpark Works

### 1. User

The process starts when the **user writes code using PySpark or SQL**.

This code becomes a **Spark application** that needs to be executed.

### 2. Driver Program

The **Driver Program** is responsible for coordinating and managing the Spark application.

The Driver Program contains important components:

- **SparkSession / SparkContext** – provides the entry point to Spark and helps the application communicate with the cluster.
- **DAG Scheduler** – creates the execution plan and divides the work into stages.
- **Task Scheduler** – schedules tasks to run on executors.
- **Catalyst Optimizer** – optimizes Spark SQL queries before execution.

The Driver requests the resources required to run the application from the **Cluster Manager**.

### 3. Cluster Manager

The **Cluster Manager** manages the resources available in the cluster.

The Driver requests resources from the Cluster Manager, and the Cluster Manager allocates the required resources for the Spark application.

Common cluster managers include:

- **Standalone**
- **YARN**
- **Kubernetes**
- **Mesos**

The allocated resources are used on the **Worker Nodes** to run Spark executors.

### 4. Worker Nodes

**Worker Nodes** are the machines that provide resources for running Spark executors.

A worker node has resources such as:

- CPU cores
- Memory

The Cluster Manager allocates these resources for the Spark application.

A worker node can run one or more **executors**, depending on how the resources are configured.

### 5. Executors

An **Executor** is a process that runs on a Worker Node.

Executors perform the actual data processing by running the tasks assigned by the Driver.

Executors:

- Run tasks assigned by the Driver.
- Process data partitions.
- Perform shuffle when required.

An executor can run multiple tasks in parallel depending on the number of CPU cores allocated to it.

For example:

```text
Executor (2 CPU cores)

Core 1 → Task 1 → Partition 1
Core 2 → Task 2 → Partition 2

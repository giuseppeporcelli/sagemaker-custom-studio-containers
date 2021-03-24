# Amazon SageMaker Custom Studio containers

Amazon SageMaker Studio architecture decuoples the JupyterServer from the actual kernels which are run on separate infrastructure and exposed via a REST interface to the JupyterServer. This architecture is enabled via Jupyter Kernel Gateway https://github.com/jupyter/kernel_gateway and the notebook extension to Kernel Gateway https://github.com/jupyter/nb2kg.

The following diagram provides an overview of the architecture:



Running a Jupyter server or any kernel in Studio corresponds to creating an App (https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_CreateApp.html). An App is characterized by its name, a type (JupyterServer or KernelGateway), the Studio domain, the user profile and the resource specification, which includes the instance type specification but, most importantly, the ARN (Amazon Resource Name) of the SageMaker Image to use.

A SageMaker Image is a versioned object that references the Docker container that runs the server or the Kernel Gateway to access one or more Jupyter kernels.

Amazon SageMaker Studio includes several pre-built images to work with the most popular ML/DL frameworks. A detailed list of images and kernels is available at https://docs.aws.amazon.com/sagemaker/latest/dg/notebooks-available-kernels.html.

However, there might be cases where it is required to build a custom container and related SageMaker Image; a typical example is using a R kernel, or supporting a newer ML/DL framework version that is not yet availalbe as pre-built images.

This repository includes examples on how to build custom containers for Amazon SageMaker Studio, create SageMaker images and make images discoverable in a Studio domain.

Each example is structured as follows:

```
example
└───docker     # Dockerfile and dependencies
└───notebook   # Notebook with detailed walkthrough 
└───scripts    # Build scripts

```

As of today, the repository contains only one example under ./basic-studio-container.
# Create a Lifecycle Configuration from the SageMaker Console<a name="studio-lcc-create-console"></a>

The following topic shows how to create a lifecycle configuration from the Amazon SageMaker console to automate customization for your Studio environment\.

## Prerequisites<a name="studio-lcc-create-console-prerequisites"></a>

Before you can begin this tutorial, complete the following prerequisite:
+ Onboard to Amazon SageMaker Studio\. For more information, see [Onboard to Amazon SageMaker Studio](https://docs.aws.amazon.com/sagemaker/latest/dg/gs-studio-onboard.html)\.

## Step 1: Create a new Lifecycle Configuration<a name="studio-lcc-create-console-step1"></a>

You can create a lifecycle configuration by entering a script from the Amazon SageMaker console\.

The following procedure shows how to create a lifecycle configuration script that prints `Hello World`\.

1. Open the Amazon SageMaker console at [https://console\.aws\.amazon\.com/sagemaker/](https://console.aws.amazon.com/sagemaker/)\.

1. From the navigation panel, under **SageMaker dashboard**, choose **Lifecycle configurations**\.

1. Choose the **Studio** tab\.

1. Choose **Create configuration**\.

1. Under **Select configuration type**, select the type of application that the lifecycle configuration should be attached to\.

1. Choose **Next**\.

1. In the section called **Configuration settings**, enter a name for your lifecycle configuration\.

1. In the **Scripts** section, enter the following content\.

   ```
   #!/bin/bash
   set -eux
   echo 'Hello World!'
   ```

1. \(Optional\) Create a tag for your lifecycle configuration\.

1. Choose **Create Configuration**\.

## Step 2: Attach the Lifecycle Configuration to Studio domain or user profile<a name="studio-lcc-create-console-step2"></a>

Lifecycle configuration scripts associated at the domain level are inherited by all users\. However, scripts that are associated at the user profile level are scoped to a specific user\. 

The following sections show how to attach a lifecycle configuration to your domain and user profile\.

### Attach to Studio domain<a name="studio-lcc-create-console-step2-domain"></a>

The following shows how to attach a lifecycle configuration to your existing domain in Studio\.

1. Open the Amazon SageMaker console at [https://console\.aws\.amazon\.com/sagemaker/](https://console.aws.amazon.com/sagemaker/)\.

1. From the left navigation panel, choose **Control panel**\.

1. From the **Control panel**, choose the **Lifecycle configurations** tab\.

1. Choose **Attach**\.

1. Under **Source**, choose **Existing configuration**\.

1. Under **Studio lifecycle configurations**, select the lifecycle configuration that you created in the previous step\.

1. Select **Attach to domain**\.

### Attach to your user profile<a name="studio-lcc-create-console-step2-userprofile"></a>

The following shows how to attach a lifecycle configuration to your existing user profile\.

1. Open the Amazon SageMaker console at [https://console\.aws\.amazon\.com/sagemaker/](https://console.aws.amazon.com/sagemaker/)\.

1. From the left navigation panel, choose **Control panel**\.

1. Under **Users**, select the user profile\.

1. From the **User Details** page, choose **Edit**\.

1. On the left navigation, choose **Studio settings**\.

1. Under **Lifecycle configurations attached to user**, choose **Attach**\.

1. Under **Source**, choose **Existing configuration**\.

1. Under **Studio lifecycle configurations**, select the lifecycle configuration that you created in the previous step\.

1. Choose **Attach to user profile**\.

## Step 3: Launch an application with the Lifecycle Configuration<a name="studio-lcc-create-console-step3"></a>

After you attach a lifecycle configuration to a user profile, the user can select it when launching an application using the Studio Launcher\. The following sections describe how to launch an application with an attached lifecycle configuration\.

1. Open the Amazon SageMaker console at [https://console\.aws\.amazon\.com/sagemaker/](https://console.aws.amazon.com/sagemaker/)\.

1. Launch the Studio Domain\. For more information, see [Use the Amazon SageMaker Studio Launcher](studio-launcher.md)\.

1. In the launcher, navigate to the **Notebooks and compute resources** section\. 

1. Select a SageMaker image\.

1. Select a start\-up script\. If there is no default lifecycle configuration, this value defaults to `No script`\. Otherwise, this value is equal to your default lifecycle configuration\. After you select a lifecycle configuration, you can view the entire script\.

1. Choose **Notebook** to launch a new notebook kernel with your selected image and lifecycle configuration\.

## Step 4: View logs for a Lifecycle Configuration<a name="studio-lcc-create-console-step4"></a>

You can view the logs for your lifecycle configuration after it has been attached to a Studio domain or user profile\. 

1. First, provide access to CloudWatch for your AWS Identity and Access Management \(IAM\) role\. Add read permissions for the following log group `/aws/sagemaker/studio` and for the following log stream `<Domain>/<UserProfile>/<AppType>/<AppName>/LifecycleConfigOnStart`\. For information about adding permissions, see [Enabling logging from certain AWS services](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AWS-logs-and-resource-policy.html)\.

1. From within Studio, navigate to the `Running instances` ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/icons/Running_squid@2x.png) tab to monitor your lifecycle configuration\. 

1. Select an application from the list of running applications\. Applications with attached lifecycle configurations have an attached indicator icon ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/studio-lcc-indicator-icon.png)\.

1. Select the indicator icon for your application\. This opens a new panel that lists the lifecycle configuration\.

1. From the new panel, select `View logs`\. This opens a new tab that displays the logs\.
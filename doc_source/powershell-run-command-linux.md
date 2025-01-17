# Running PowerShell scripts on Linux managed nodes<a name="powershell-run-command-linux"></a>

Using the `aws:runPowerShellScript` plugin or the `AWS-RunPowerShellScript` command document, along with PowerShell Core, you can run PowerShell scripts on Linux managed nodes\. This can be useful for systems administrators who are familiar with PowerShell and prefer it to other scripting languages\.

**Before you begin**  
Connect to your Linux managed node and follow the [PowerShell Core](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6) installation procedure for the appropriate operating system\.

Many PowerShell commands \(cmdlets\) aren't available on Linux\. To see which commands are available, use the `Get-Command` cmdlet after starting PowerShell using the `pwsh` command on your Linux managed node\. For more information, see [Get\-Command](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-command?view=powershell-6)\. 

The following procedure describes how to run a PowerShell script on a Linux managed node using the console\.

**To run a PowerShell script on a Linux managed node using the console**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation pane, choose **Run Command**\.

   \-or\-

   If the AWS Systems Manager home page opens first, choose the menu icon \(![\[Image NOT FOUND\]](http://docs.aws.amazon.com/systems-manager/latest/userguide/images/menu-icon-small.png)\) to open the navigation pane, and then choose **Run Command**\.

1. Choose **Run command**\.

1. In the **Command document** list, choose the `AWS-RunPowerShellScript` document\.

1. In the **Command parameters** section, specify the available PowerShell commands you want to use\.

1. In the **Targets** section, choose the managed nodes on which you want to run this operation by specifying tags, selecting instances or edge devices manually, or specifying a resource group\.
**Note**  
If a managed node you expect to see isn't listed, see [Troubleshooting managed node availability](troubleshooting-managed-instances.md) for troubleshooting tips\.

1. For **Other parameters**:
   + For **Comment**, enter information about this command\.
   + For **Timeout \(seconds\)**, specify the number of seconds for the system to wait before failing the overall command execution\. 

1. For **Rate control**:
   + For **Concurrency**, specify either a number or a percentage of managed nodes on which to run the command at the same time\.
**Note**  
If you selected targets by specifying tags applied to managed nodes or by specifying AWS resource groups, and you aren't certain how many managed nodes are targeted, then restrict the number of targets that can run the document at the same time by specifying a percentage\.
   + For **Error threshold**, specify when to stop running the command on other managed nodes after it fails on either a number or a percentage of nodes\. For example, if you specify three errors, then Systems Manager stops sending the command when the fourth error is received\. Managed nodes still processing the command might also send errors\.

1. \(Optional\) For **Output options**, to save the command output to a file, select the **Write command output to an S3 bucket** box\. Enter the bucket and prefix \(folder\) names in the boxes\.
**Note**  
The S3 permissions that grant the ability to write the data to an S3 bucket are those of the instance profile \(for EC2 instances\) or IAM service role \(on\-premises machines\) assigned to the instance, not those of the IAM user performing this task\. For more information, see [Create an IAM instance profile for Systems Manager](setup-instance-profile.md) or [Create an IAM service role for a hybrid environment](sysman-service-role.md)\. In addition, if the specified S3 bucket is in a different AWS account, make sure that the instance profile or IAM service role associated with the managed node has the necessary permissions to write to that bucket\.

1. In the **SNS notifications** section, if you want notifications sent about the status of the command execution, select the **Enable SNS notifications** check box\.

   For more information about configuring Amazon SNS notifications for Run Command, see [Monitoring Systems Manager status changes using Amazon SNS notifications](monitoring-sns-notifications.md)\.

1. Choose **Run**\.

To see examples that use the `aws:runPowerShellScript` plugin, see [`aws:runPowerShellScript`](ssm-plugins.md#aws-runPowerShellScript)\.
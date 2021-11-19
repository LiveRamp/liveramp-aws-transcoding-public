# Overview
LiveRamp’s Embedded Transcoder allows for the conversion of RampID from one encoding to RampID in another partner encoding.  This conversion takes place inside an AWS Virtual Private Cloud (VPC) so that the data never leaves your control, with attendant latency and security benefits. Transcoding requires the agreement of both parties, owners of each domain.

LiveRamp’s AWS Embedded Transcoder deployment invokes [SageMaker’s network isolation mode](https://aws.amazon.com/blogs/security/secure-deployment-of-amazon-sagemaker-resources/) on the appliance, protecting your VPC and deployed LiveRamp technology. The system design forces all interactions between the encryption technology and your VPC through a proxy service.  This proxy also handles authentication requirements and updates to the appliance.

[This deployment guide](https://github.com/hansfrederickbrown/liveramp-aws-transcoding-public/blob/patch-1/docs/AWS%20Embedded%20Transcoder%20Deployment%20Guide.pdf)This deployment guide details how to initialize the appliance using a CloudFormation template, walks you through authentication, and describes how to call the transcoding service. The document walks through additional details on the architecture and design, and provides additional resources for review.
The steps for deploying LiveRamp’s Embedded Transcoder are:

1. Subscribe to LiveRamp’s Embedded Transcoder product through the AWS Marketplace.
2. Execute multi-party agreements through LiveRamp for data exchange.
3. Download the template from the [public Github repository](https://github.com/LiveRamp/liveramp-aws-transcoding-public).
4. Run the template in AWS CloudFormation
5. Run the LiveRamp /init endpoint to initialize the transcoder.
6. Get a Smart Token from SM Proxy’s /request endpoint. Tokens must be refreshed every 15 minutes by calling the /request endpoint and passing the rpc parameter the value refresh. The system must also be reinitialized every day after 6 AM CST (UTC -6:00).
7. Use the SageMaker proxy /request endpoint to execute the transcoding; client_id, client_secret, and the rpc parameter set to request as parameters of the call.

A typical use case for Transcoding is the ability to unlock collaboration use cases by translating an encoded RampID to a partner’s encoding (or vice versa).  By leveraging LiveRamp’s Embedded Transcoder offering, you’re able to translate across identity spaces to drive actionable insights.

The Embedded Transcoder allows you to connect your LiveRamp identities with external datasets to solve problems of interest. Brands and platforms want to connect, control, and activate data quickly and securely across the advertising technology marketplace but are faced with security concerns and latency issues making it difficult to connect and take action on customer data.

# Audience
This document is intended for existing LiveRamp customers with data already resolved to RampID looking for a way to translate to a partner encoded RampID within their own AWS VPC. The following sections will walk you through the deployment process starting in AWS Marketplace, downloading the CloudFormation template, and instantiating the Transcoder appliance. The audience is a data engineer tasked with transcoding.

# Prerequisites
LiveRamp’s Embedded Transcoder offering is available through the AWS Marketplace and deployed through a [CloudFormation](https://aws.amazon.com/cloudformation/) template that is stored in a GitHub repository. 
The following prerequisites are needed:
1. Access to a public GitHub repository.
2. An AWS Marketplace account and ability to procure through the Marketplace.
3. Access to [CloudFormation](https://aws.amazon.com/cloudformation/) and the ability to create [IAM](https://aws.amazon.com/iam/) roles and resources.
4. Customer data already resolved to RampID, this service will transcode from one RampID encoding to another.
5. Multi-party consent is required, both parties need to execute a LiveRamp permission order for access to be permitted to transcode to a partner RampID encoding.
 
# Product Support
Support for Embedded Transcoder can be found on the following:  [developer site](https://developers.liveramp.com/retrieval-api/reference#transcode-rampids-1), [community support site](https://support.liveramp.com/) and by working with your LiveRamp account team.  LiveRamp’s Embedded Transcoder deployment is supported by our Global Support team, a 24/7 operation to provide the first line of defense on technical issues.  Support for this product will be limited to interactions between the proxy and our encoding technology (including incoming requests) and from the proxy out to our core services (authorization requests and updates).  Other support issues involving AWS technology will need to be directed to the AWS support team.

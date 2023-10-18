# AWS Network Architecture Overview 🌐

## Table of Contents 📚

- [Introduction](#introduction) 📖
- [Live Demo](#live-demo) 🎥
- [Components](#components) 🛠️
  - [Route 53](#route-53) 🌐
  - [AWS Shield](#aws-shield) 🛡️
  - [AWS WAF](#aws-waf) 🚫
  - [Application Load Balancer (ELB)](#application-load-balancer-elb) ⚖️
  - [EC2 Instances](#ec2-instances) 🖥️
  - [CloudFront](#cloudfront) ☁️
  - [Network ACL](#network-acl) 🔒
  - [VPC and Subnets](#vpc-and-subnets) 🌐
- [Data Flow](#data-flow) 📈

## Introduction 📖

This document describes the AWS network architecture that has been designed to be highly available and secure. This architecture includes various AWS services like Route 53, Application Load Balancer (ELB), EC2 instances, AWS Shield, AWS WAF, and CloudFront.

## Live Demo 🎥

Interested in seeing this AWS Network Architecture in action? You can view the live-action diagram [here](https://tsmith4014.github.io/I-Animated-AWS-Network-diagram/). Feel free to explore the various components and their interactions and don't forget to wave to the stick figure folks. 👋

## Components 🛠️

### Route 53 🌐

- Provides DNS routing for the application.
- Routes incoming traffic through AWS Shield and AWS WAF before passing it on to the Application Load Balancer.

### AWS Shield 🛡️

- Provides DDoS protection for the architecture.
- Integrated with Route 53 to filter traffic at the DNS level.

### AWS WAF 🚫

- Web Application Firewall that protects the application from web exploits.
- Also integrated with Route 53 to provide another layer of security filtering.

### Application Load Balancer (ELB) ⚖️

- Distributes incoming application traffic across multiple targets, such as EC2 instances.
- Located in a designated public subnet.
- No direct Network ACLs around the ELB itself, but there are Network ACLs between the ELB and the EC2 instances.

### EC2 Instances 🖥️

- Virtual machines to run the application.
- Located in separate public and private subnets for increased security.
- Autoscaling is enabled for high availability.

### CloudFront ☁️

- CDN service that caches and serves application content.
- Integrated directly with the ELB for caching and content distribution.

### Network ACL 🔒

- Provides a layer of security that acts as a firewall for controlling traffic in and out of the VPC and subnets.
- Placed between the Application ELB and EC2 instances.

### VPC and Subnets 🌐

- VPC isolates the AWS resources and defines the network topology.
- Public and private subnets used to segregate resources and manage traffic routing through Network ACLs and route tables.

## Data Flow 📈

1. **Route 53** receives the incoming traffic and routes it through **AWS Shield** and **AWS WAF**.
2. The filtered traffic then hits the **Application ELB**.
3. **Application ELB** routes the traffic to the appropriate **EC2 instances**.
4. **CloudFront** can also route cached content directly to the ELB.


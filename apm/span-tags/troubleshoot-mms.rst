.. _troubleshoot-mms:

**********************************************************************
Troubleshoot cardinality in Monitoring MetricSets 
**********************************************************************

.. Metadata updated: 1/23/23

.. meta::
   :description: Learn how to troubleshoot cardinality using Monitoring MetricSets.

Follow these steps to troubleshoot issues with high cardinality and Monitoring MetricSet configurations. 

Troubleshoot high cardinality data
===================================

If the cardinality of your Monitoring MetricSets is high, you might reach your subscription limits and be unable to create new Monitoring MetricSets. This page provides guidance on how to configure your Monitoring MetricSets with efficiency. 

Choose between service and endpoint level MetricSets
---------------------------------------------------------

The following table outlines the difference between endpoint and service level MetricSets. 

.. list-table::
      :header-rows: 1
      :widths: 50 50

      * - :strong:`Endpoint level MetricSet`
        - :strong:`Service Level MetricSet`
    
      * - * If you already know which endpoints you're interested in, start with an endpoint level MetricSet to help reduce the cardinality of your MetricSet
          * To choose a subset of endpoints, you can add a list or write a regular expression pattern to match the endpoints you want to track 
        - * If you are interested in metrics about the overall health of you service, start with a a service level MetricSet 
          * The Monitoring MetricSets at the service level are an aggregation of the metric sets at the endpoints level
          * If you don’t specify any filters, then the tag is added to all of the endpoints for the Monitoring MetricSet for the service




The Monitoring MetricSets at the service level are an aggregation of the metric sets at the endpoints level. If you specify the endpoints that are of interest to you in your Monitoring MetricSet, then you can reduce the amount of data.

However, limiting the number of endpoints in your Monitoring MetricSet isn’t always a guaranteed way to reduce your cardinality. 

.. _reduce-cardinality: 

Guidance on how to reduce cardinality 
========================================
If you have high cardinality metrics that exceed the system limit or subscription quota for your contract, try these methods to reduce cardinality for your metric set: 

* Turn off an endpoint MetricSet by choosing Service MMS only.
* Add a filter by tag value to reduce the number of results.
* Remove or filter down existing Monitoring MetricSets. The cardinality check in APM estimates your total cardinality of existing MMS in addition to your proposed changes.  
* MetricSets with zero cardinality are not considered valid. If you have zero cardinality, verify that your configuration details are correct, or try again once you are ingesting the relevant tracing data. 
* If the Monitoring MetricSet times out, try adding filters and running it again. 
* Provide a list of tag values, or a regular expression.

For more information on troubleshooting high and low cardinality, see :ref:`Guidelines for working with low and high cardinality data<guideline-cardinality>`. 


Example: How to reduce cardinality through tag filters  
--------------------------------------------------------
In this example, the custom dimension is :code:`customer.id`. 

For example, suppose you want to track a checkout workflow on your application. In your environment, this workflow is called the checkout service. You create a Monitoring MetricSet with two endpoints, add-to-cart, and checkout. However, you find that your cardinality is quite high for the Monitoring MetricSet for these two endpoints because there are 10k unique customer IDs for the :code:`customer.id` tag associated with these endpoints.To reduce the overall cardinality for this Monitoring Metricset, you can filter by tag values to a smaller subset of customer IDs that are of interest to you instead of needlessly processing 10k unique tags.


Check that your Monitoring MetricSet is set up correctly 
======================================================================
After you set up your Monitoring MetricSet, go to the APM Troubleshooting MetricSet Configuration page to make sure that the status is active. Once your MMS is active, you will start seeing metrics as soon as matching traces arrive.

For guidance:
 * When and why you might want to pause, or stop, your MetricSet, see :ref:`Status of configured  MetricSets<tms-status>`. 
 * How to :ref:`Manage existing Monitoring MetricSets<manage-TMS>`.
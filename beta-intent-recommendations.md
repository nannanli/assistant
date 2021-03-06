---

copyright:
  years: 2015, 2020
lastupdated: "2020-01-29"

subcollection: assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Beta: Intent recommendations
{: #beta-intent-recommendations}

Let Watson analyze your chat transcript log data to understand the most common and frequently expressed customer needs related to your business. Watson can then recommend intents and intent user examples you can use to train your assistant so it can recognize the same and similar requests in the future.
{: shortdesc}

![Plus or Premium plan only](images/plus.png) When generally available, it will be available to Plus or Premium plan users only.
{: note}

Watson can recommend some initial intents for you to start with. Or, if you already created some intents, Watson analyzes your logs and compares its findings with your existing intents to identify gaps in your training data and suggest new intents that can fill them in. 

The abiility to use assistant logs as the source for intent recommendations is available for use by participants in the early access program only. To find out how to request access, see [Participate in the early access program](/docs/assistant?topic=assistant-feedback#feedback-beta).
{: preview}

When you participate in the early access program, IBM gives you early access to features for your evaluation. These features are classified as beta, which means they might be unstable, might change frequently, and might be discontinued with short notice. Beta features also might not provide the same level of performance or compatibility that generally available features provide and are not intended for use in a production environment. Beta features are supported only on the [IBM Developer Answers](https://developer.ibm.com/answers/topics/watson-assistant/){: external}.

## Get help getting started
{: #intent-recommendations-get-started}

Customer needs are represented in {{site.data.keyword.conversationshort}} as *intents*. If you have not defined intents yet, you can get started faster by getting Watson to help you. Upload a file that contains the utterances that customers use to articulate requests when they interact with your customer support personnel. You might be able to extract these utterances from call center transcripts, for example. Upload the utterances as a CSV file to {{site.data.keyword.conversationshort}} so that Watson can analyze the data. Based on the insights it uncovers, Watson recommends a base set of intents you should build to cover the most common needs of your customers.

The following video provides a 3 1/2-minute overview of intent and intent user example recommendations.

An earlier version of the product was used to recored this video. As a result, the look and placement of some of the user interface elements is different. Also, it does not show support for adding recommendations by using an assistant's logs as the source.
{: note}

<iframe class="embed-responsive-item" id="youtubeplayer" title="Intent recommendations overview" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/64h59KqDY98?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

To learn more about how intent recommendations can help you build a useful bot faster, [read this blog post ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://medium.com/ibm-watson/let-watson-train-your-virtual-assistant-57bd53b12bc3){: new_window}.

## Keep your training data current
{: #intent-recommendations-stay-current}

As the subjects that your customers want to discuss change, you can use the intent and intent user example recommendations features to help keep your intents relevant over time.

Not only can Watson analyze real-world utterances extracted from customer support site chat log transcripts, but you can also configure Watson to use the logs that are generated by your assistant as it interacts with your customers. 

Mine your existing data to do one of the following things:

- [Get intent recommendations](#intent-recommendations-get-intent-recommendations-task)
- [Get intent user example recommendations](#intent-recommendations-get-example-recommendations-task)

See [Supported languages](/docs/assistant?topic=assistant-language-support) for information about the language support for this feature.

## Enabling the intent recommendations feature
{: #intent-recommendations-enable-task}

The first time you use intent recommendations, you must enable the feature and add at least one recommendation data source.

1.  Open your dialog skill.

1.  From the skill menu, click **Intents**.

1.  Click **View intent recommendations**.

1.  Choose the type of recommendation data source you want to use.

## Managing recommendation sources
{: #intent-recommendations-data-resources}

Intent recommendations are based on analysis of real-world user utterances, which you can provide in uploaded CSV files or by connecting to the log of a deployed assistant.

- [Live assistant log](#intent-recommendations-live-assistant-add): The log from an assistant that is deployed and is actively interacting with customers
- [CSV log files](#intent-recommendations-log-files-add): A list of utterances that is extracted from support center chat transcripts.

You must choose a recommendation source type; you cannot use both.

The recommendation source data that you add is used to derive both intent and intent user example recommendations.

### Getting recommendations from an assistant log
{: #intent-recommendations-live-assistant-add}

To use assistant chat logs as the source for your intent and intent user example recommendations, the assistant must meet these requirements:

- The assistant must be *live*, meaning it is deployed in a production environment, and is interacting with customers.
- The application with which you deploy the assistant must use the v2 `/message` API. The log of an assistant that receives user input through the v1 `/message` API cannot be used as a recommendation source. 

  All of the built-in integrations use the v2 API. See [Adding integrations](/docs/assistant?topic=assistant-deploy-integration-add).
  {:tip}
- The assistant must have exchanged messages with a customer within the log retention time period. Logs are stored for a number of days, the total of which is determined by your service plan type. If no customer interactions take place within the retention period, then there is no log data available to use as a recommendation source. For details about log limits, see [Log limits](/docs/assistant?topic=assistant-logs#logs-limits).
- The assistant log must contain at least 3,000 messages.

{{site.data.keyword.Bluemix_dedicated_notm}}: You cannot get intent recommendations from logs. You can see the option to link to a connected log, but the data source will always indicate that there are 0 logs available. To use an assistant log as the source for your intent recommendations, switch to a Premium plan. Alternatively, you can add the user utterances from the logs to a CSV file, upload it, and choose the logs CSV file as the data source.

### Getting recommendations from a CSV log file
{: #intent-recommendations-log-files-add}

To share your support center chat log transcript data with Watson, you must upload the data as a CSV file in the correct format. Create a comma-separated value (CSV) file with one customer utterance per line. Ideally, the utterances are short phrases which are extracted from your call center transcripts that contain real-world customer questions and requests. 

Each user example source file can be a maximum size of 20 MB.

Follow these additional guidelines:

  - Remove any sensitive data from the utterances that you include in the file.

    Sensitive data includes any information relating to an identifiable natural person such as names, email addresses, and customer IDs, and regulated data such as protected health information.
    {: important}
  
  - Do not include utterances that exceed 1,024 characters in length. Longer utterances are truncated.
  - The file must contain at least 100 utterances; a file with 500 or more utterances will give you better results.
  - If an utterance contains a comma, surround the utterance in quotation marks.
  - The CSV must include only one column.
  - Remove everything that is not a customer-generated utterance, including any human agent responses or notes.

  For example:

  ```
  What happens to my coverage if I trade in my car?
  i'd like to buy a house.
  How do I add a dependent to my plan?
  "first, i want to know if i am already registered."
  ```

Any files you upload are shared across all of the skills in the current service instance. The utterances from all of the available files are mined when you ask for both intent recommendations and intent user example recommendations.

#### Should I copy edit the CSV log file?
{: #beta-intent-recommendations-copy-edit}

It helps if the user utterances that serve as the source for intent user examples have accurate spelling and grammar.
When users interact with the live assistant, many of the misspellings they make in their input are autocorrected. So, if you have clear and correct user examples, the input that is processed at run time is easier to map to the appropriate intents.

However, do not run a spell check tool over the CSV file you create as the user example source file. A dumb spell check tool will do more harm than good. The reason is that it will not preserve terms that are unique to your domain.

For example, DUCS is an acronym for Display Unit Control System, which was an early teleprocessing monitor. Maybe that acronym has meaning to your domain. If so, you don’t want a spell checker to replace every occurrence of *DUCS* with the word *ducks*. It will clearly change the meaning of the utterance. In fact, the autocorrection function uses the existing training data to identify domain-specific terms that should not be corrected. 

If you choose to correct spelling and grammar in the user examples, follow these tips:

- Get a human subject matter expert to do a visual copy edit of the utterances.
- To minimize the effort, do a copy-edit pass on only the subset of recommended utterances that are chosen to be added to the training data.

Doing a copy edit is not required. If there are misspellings in your training data, the autocorrection tool will accept the misspelled words at run time and still be able to classify input successfully. You might be perpetuating a misspelling, but doing so will have limited impact on the overall performance of your assistant.
{: note}

For more information about how autocorrection works, see [Correcting user input](/docs/assistant?topic=assistant-dialog-runtime#dialog-runtime-spell-check)

## Getting intent recommendations
{: #intent-recommendations-get-intent-recommendations-task}

Before you begin, you must [enable the intent recommendations feature](#beta-intent-recommendations-enable-task). 

After the data is provided, Watson evaluates the user utterances and identifies common problem areas that customers mention frequently. {{site.data.keyword.conversationshort}} then displays a set of discrete intents that capture the trending customer needs. You can review each recommended intent and its corresponding user examples to choose the ones you want to add to your training data.

To get intent recommendations, complete the following steps:

1.  Open your dialog skill.

1.  From the skill menu, click **Intents**.

1.  Click **View intent recommendations**.

    Give Watson time to analyze your data and group the utterances.

1.  Review the intents that are recommended by Watson.
    
    If your recommendation source has over 500,000 user utterances, then Watson samples the data and derives recommendations from the sampled subset.

    The top intent recommendations are chosen and ordered as follows:

    - Intents with the most frequently occuring utterances. The frequency of the utterances associated with these intents suggests they identify the most common customer pain points.
    - The distinctness of the newly recommended intents when compared to the intents that are already in your training data. Their uniqueness suggests that they can address customer needs that are not being met currently.
    - The similarity of the user examples that are associated with the intent, which illustrates the strength of the intent.

1.  Click an intent to see its associated user examples.

    Watson chooses a maximum of 20 user examples for each intent it recommends. It deduplicates examples from the source, and limits the overall number of utterances to a set of top user examples to make it easier for you to understand and work with them.

1.  Select any utterances that you want to add to your training data, and then perform one of the following tasks:

    - To add the recommended intent with the selected utterances as user examples, click **Create new intent**.
    - To add the selected utterances from the recommended intent to one of your existing intents as user examples instead, click **Add to existing intent**, choose the intent, and then click **Add**.

The intents and intent user examples that you add in this way do count toward your intent and intent user example totals for which there are limits per plan. See [Intent limits](/docs/assistant?topic=assistant-intents#intents-limits) for more details.

As the subjects that your customers want to discuss change, you can use the intent user example recommendations feature to help keep your intents up-to-date and revelant over time.

## Intent user example recommendations
{: #intent-recommendations-get-example-recommendations-task}

For any intent that is already part of your training data, you can find and add new user examples by asking Watson for intent user example recommendations. 

Before you begin, you must [enable the intent recommendations feature](#intent-recommendations-enable-task). Even though you request user example recommendations on a per-intent basis, the same data source is used to find user examples that are appropriate for every intent. Watson knows which intent you are working on and finds suitable examples to recommend for that specific intent.

1.  Follow the steps in [Creating intents](/docs/assistant?topic=assistant-intents#intents-creating-intents-task) to create an intent.

1.  Add at least 5 user examples that illustrate the full range of typical utterances that you anticipate customers might say to trigger this intent.

    These *seed* user examples teach Watson about the kinds of utterances to look for in the recommendation source data you provided.

1.  Click **Show recommendations**.

    Recommended user examples are displayed in the side panel.
    
    If no recommendations are made, then the connected recommendation source does not contain examples that are suitable for this intent.

1.  If the current recommendation source cannot provide useful recommendations for any of your intents, you can try a different set of utterances by changing the recommendation source that you're using. See [Managing recommendation sources](#intent-recommendations-data-resources) for more details.

1.  After Watson shows you recommendations, select the utterances that you want to add as user examples for this intent, and then click **Add**. Or click **Next set** to review more utterances.
1.  If you want to search the content of the recommendation source for user examples yourself, click the **Search Logs** tab. Enter a keyword on which to base the search, and then press **Enter**.

    Follow these search query syntax guidelines:

    - Boolean operators (such as `AND` and `OR`) are supported.
    - Add quoted text to search for an exact text match ("thisstringmustbepresent").
    - You can use regular expressions, such as `*ly` to find all terms that end with `ly`.
    - The following characters are used as regular expression operators:

      `+ - = && || > < ! ( ) { } [ ] ^ " ~ * ? : \ /`

      If you want to include one in a search term without it being processed as an operator, you must prefix it with a backslash (`\`).

The user examples that you add in this way do count toward your intent user example totals for which there are limits per plan. See [Intent limits](/docs/assistant?topic=assistant-intents#intents-limits) for more details.

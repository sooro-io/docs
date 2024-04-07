---
navigation:
  order: 1
  title: Advanced Event ID
---

# Advanced Event ID

This GTM variable template allows you to generate a unique event ID.

The variable is particularly helpful if you are using a hybrid approach in your tracking. Means when you are using client and server-side tracking in parallel. In this scenario events can be tracked twice what you want to avoid.

The solution for it is the so-called event deduplication. To deduplicate events an identifier is necessary which is often an event ID. As a result you need to have unique event ID for each single event you track. Unfortunately such an ID is often not available.

Our template helps you to solve this problem by creating event IDs for you.

## How it works

An event ID can be created by using different available data points. The good news is that the GTM itself provides a few very useful information for this task. But if you only use these, an ID collision could easily occur. In other words, the case that two identical IDs are generated. To avoid this, another element comes into play to ensure the uniqueness of the event ID.

In our template we use the following data points to create the event ID:

- uniqueness element (a client ID or something similar)
- GTM start time
- GTM unique event id (not so unique as it sounds)

If an element is not available, there is always a fallback. This ensures that a unique event ID can almost always be created.

## Configuration

Configuring the variable should be quick as there are only a few options. But they are powerful enough that you only need to create a single event ID variable in the entire GTM container.

### Uniqness Element

This element ensures that the event ID is unique. Ideally, there is a client ID in your tracking that you can use for this.

If not, you can also choose the option to generate an ID based on a random number and a timestamp. We recommend that the uniqeness element is as static as possible for a single client. Thus, the template offers two options for caching. You can also disable caching completely if you have privacy concerns.

#### Caching Options

**temporary**  
The uniqueness element is temporarily cached in the window object of the browser. It gets deleted as soon as the tab or browser will be closed.

**persistent**  
The uniqueness element is cached in the localStorage of the browser. The value therefore remains the same across several sessions and even across tabs in the users browser.

<Blockqoute type="warning">
If you use the **persistent** option, information is stored permanently on the user’s device. It may therefore be necessary to adapt the information in your consent banner and/or privacy policy to comply with legal requirements.
</Blockqoute>

<Blockqoute type="tip">
If you choose a caching option, you will find the generated value under the `gtmClientId` key (either in the window object or the localStorage). Since the generated value is something like a client ID, it might help you in another place.
</Blockqoute>

### Override Rules

There are always situations where a unique event ID that comes from your systems is an advantage. For example, the user can reload a specific page so that tracking is triggered again. For important events (e.g. purchase) this would lead to a distortion in reporting or the optimization of marketing campaigns. To get around this problem, we offer the option of overwriting the event ID directly in the variable.

**use GA4 transaction ID**  
If your tracking is based on GA4 events, you can use the transaction ID specified in the purchase event.

**Special IDs**  
You can enter as many entries as you want here when you want to use your own event ID. To do this, enter the event name and your existing ID.

## Good to know

There are various fallbacks in the template code so that an event ID is always generated. Therefore, an undefined value in one of your inputs is not a problem.

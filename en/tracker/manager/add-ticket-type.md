# Configure issue types

{% note warning %}

By default, [only the queue owner](queue-access.md) can configure a queue.

{% endnote %}

A queue may include different types of issues, such as <q>New feature</q>, <q>Improvement</q>, or <q>Bug</q>. Each type of issue has its own workflow and set of resolutions. You can change the parameters of the available types of issues in the queue settings.

## Add an issue type to a queue{#section_mvh_5yb_gz}

To create a new issue type:

1. Go to the queue page.

1. Select ![](../../_assets/tracker/icon-settings.png) → **Administration**.

1. Go to the **Issue types** tab.

1. Click **Add issue type**.

1. Configure settings:
    - **Issue type**: Select one of the available types.
      The most popular issue types are available in {{ tracker-name }} by default. If you don't see the type you need, your company's admin can [create it](create-ticket-type.md).
    - **Workflow**: Set the workflow to apply to this type of issue. Select one of the available workflows or [create a new one](add-workflow.md) based on one of them.
    - **Resolutions**: Select possible resolutions.
     The most popular resolutions are available in {{ tracker-name }} by default. If you don't see the resolution you need, your company's admin can [create it](create-resolution.md).
	 

1. The **Statuses and transitions** section shows the main parameters of the selected workflow. If necessary, you can edit it or create a copy.

1. Click **Save** at the bottom of the tab.

## Remove an issue type from the queue {#section_czj_jqm_2bb}

If one of the issue types is no longer needed in the queue, you can remove it.

{% note warning %}

You can only remove types that are not used for any of the issues in the queue.

{% endnote %}

To remove an issue type from a queue:

1. Go to the queue page.

1. Select ![](../../_assets/tracker/icon-settings.png) → **Administration**.

1. Go to the **Issue types** tab.

1. To remove the type, click ![](../../_assets/tracker/remove-task-type.png).

1. Click **Save** at the bottom of the tab.


[Contact support](../troubleshooting.md)


---
description: Datasets and Views (Beta)
---

# Datasets and Views

{% hint style="info" %}
Self-managed Datasets and Views is in beta for Design Partners. Get in touch for more info.
{% endhint %}

The Spice.ai platform comes pre-loaded with a variety of web3 [datasets](../../datasets.md).

In addition, you can define and create your own private Datasets and Views, which can then be queried with SQL, cached in Spice Firecache, and published publicly to be shared with others.

### Defining a Dataset

To define a dataset, first ensure your Spice app is connected to a [GitHub repository](link-github-repository-beta.md), then add a [dataset manifest](../../reference/specifications/dataset-and-view-yaml-specification/) file to the GitHub repository in the `.spice/datasets` path.

For example:

```yaml
# .spice/datasets/recent_blocks.yml
name: eth.recent_blocks
type: append
firecache:
  enabled: true
  trigger: number
  time_column: timestamp
```

See the [Dataset & View YAML Specification](../../reference/specifications/spice-functions-yaml-specification/) for the full YAML schema.

### Sync with GitHub

Once the manifest file is committed to the GitHub repository, navigate to the **Datasets** section of the **Hub**, and click **Sync with GitHub**. The newly defined dataset will appear in the datasets list.

<figure><img src="../../.gitbook/assets/image (2) (2).png" alt=""><figcaption><p>List of synced Datasets in the Hub.</p></figcaption></figure>

### Deploy the Dataset

Click the dataset **Deploy** button. Because this dataset was Firecache enabled, the firecache status will now turn to **Ready.**

<figure><img src="../../.gitbook/assets/image (1) (2) (1).png" alt=""><figcaption><p>Deployed dataset eth.recent_blocks is now firecache Ready.</p></figcaption></figure>

### View Dataset details

Clicking the dataset will show its details along with it's deployments.

<figure><img src="../../.gitbook/assets/image (1) (3).png" alt=""><figcaption><p>Dataset details page.</p></figcaption></figure>


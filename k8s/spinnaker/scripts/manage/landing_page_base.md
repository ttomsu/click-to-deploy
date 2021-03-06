# Manage Spinnaker

Use this section to manage your Spinnaker deployment going forward.

## Select GCP project

Select the project in which your Spinnaker is installed, then click **Confirm
project**.

<walkthrough-project-billing-setup>
</walkthrough-project-billing-setup>

## Manage Spinnaker via Halyard from Cloud Shell

This section guides you as you manage your Spinnaker deployment.

### Ensure you are connected to the correct Kubernetes context

```bash
PROJECT_ID={{project-id}} ~/click-to-deploy/k8s/spinnaker/scripts/manage/check_cluster_config.sh
```

### Pull Spinnaker config

Paste and run this command to pull the configuration from your Spinnaker
deployment into your Cloud Shell.


```bash
~/click-to-deploy/k8s/spinnaker/scripts/manage/pull_config.sh
```

### Update the console

**This is a required step if you've just pulled config from a different Spinnaker deployment.**

This will include details on how to connect to Spinnaker.

```bash
~/click-to-deploy/k8s/spinnaker/scripts/manage/update_console.sh
```

### Configure Spinnaker via Halyard

All [halyard](https://www.spinnaker.io/reference/halyard/commands/) commands are available.

```bash
hal config
```

As with provisioning Spinnaker, don't use `hal deploy connect` when managing
Spinnaker. Also, don't use `hal deploy apply`. Instead, use the `push_config.sh`
and `apply_config.sh` commands shown below.

### Notes on Halyard commands that reference local files

If you add a Kubernetes account that references a kubeconfig file, that file must live within
the '`~/.hal/default/credentials`' directory on your Cloud Shell VM. The
kubeconfig is specified using the `--kubeconfig-file` argument to the
`hal config provider kubernetes account add` and ...`edit` commands.

Change the `default` path segment if you are using a different name for your deployment.

The same requirement applies for any Google JSON key file specified via the
`--json-path` argument to various commands.

### Push updated config to Spinnaker deployment

If you change any of the configuration, paste and run this command to push
those changes to your Spinnaker deployment.

```bash
~/click-to-deploy/k8s/spinnaker/scripts/manage/push_config.sh
```

### Apply updated config to Spinnaker deployment

After you push configuration changes, you need to paste and run the following
command to apply them to your Spinnaker deployment.

```bash
~/click-to-deploy/k8s/spinnaker/scripts/manage/apply_config.sh
```

## Included command-line tools

### Halyard CLI

The [Halyard CLI](https://www.spinnaker.io/reference/halyard/) (`hal`) and
daemon are installed in your Cloud Shell.

If you want to use a specific version of Halyard, use `~/click-to-deploy/k8s/spinnaker/scripts/cli/install_hal.sh`.
If you want to upgrade to the latest version of Halyard, use `~/click-to-deploy/k8s/spinnaker/scripts/cli/update_hal.sh`.

### Spinnaker CLI

The [Spinnaker CLI](https://www.spinnaker.io/guides/spin/app/) 
(`spin`) is installed in your Cloud Shell.

If you want to upgrade to the latest version, use `~/click-to-deploy/k8s/spinnaker/scripts/cli/install_spin.sh`.

## Scripts for Common Commands

### Add Spinnaker account for GKE

Before you run this command, make sure you've configured the context you intend
to use to manage your GKE resources.

The public Spinnaker documentation contains details on [configuring GKE
clusters](https://www.spinnaker.io/setup/install/providers/kubernetes-v2/gke/).

```bash
~/click-to-deploy/k8s/spinnaker/scripts/manage/add_gke_account.sh
```

### Add Spinnaker account for GCE

```bash
~/click-to-deploy/k8s/spinnaker/scripts/manage/add_gce_account.sh
```

### Connect to Redis

```bash
~/click-to-deploy/k8s/spinnaker/scripts/manage/connect_to_redis.sh
```

## Configure Operator Access

To add additional operators, grant them the `Owner` role on GCP Project {{project-id}}: [IAM Permissions](https://console.developers.google.com/iam-admin/iam?project={{project-id}})

Once they have been added to the project, they can locate Spinnaker by navigating to the newly-registered [Kubernetes Application](https://console.developers.google.com/kubernetes/application/$ZONE/$DEPLOYMENT_NAME/spinnaker/$DEPLOYMENT_NAME?project={{project-id}}).

The application's *Next Steps* section contains the relevant links and operator instructions.


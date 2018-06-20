# Launching a Google Compute Instance via the API
You can never find enough of these tutorials/examples lying around, so here's one in golang borrowing heavily from [google's own examples](https://github.com/google/google-api-go-client/tree/master/examples).

## Create a Service Account
- Navigate to the IAM & admin" section of your project and select ["Service Accounts"](https://console.cloud.google.com/iam-admin/serviceaccounts)
- Create a new Account including the roles "Compute Admin" & "Service Account User"
- Ask for a new private key for download in JSON format

## Extract and export your credentials
- In the downloaded JSON file, you'll see "client_email" & "private_key"
- `$ export GCE_EMAIL=<client_email value>`
- `$ export GCE_PRIVATE_KEY='<private_key value>'`
- keep in mind that some deploy services (looking at you, CircleCI) add these behind the scenes (meaning double single quotes and an incorrect key)

## Play with the hardcoded bits
- This sample file launches an [f1-micro instance named 'bluesbros2', running CoreOS in us-east-1](./main.go#L58) in **my project**
- Please adjust to your needs ;)
- Here's the [list of OS images](https://console.cloud.google.com/compute/images)
- us-east-1 & f1-micro is special because you basically get [one freebie / month](https://cloud.google.com/free/docs/always-free-usage-limits#compute_name)!

## Launch your instance
- simply executing `go run main.go` will launch your instance

## SSH & gcloud access
- Before launching, you can add your own [SSH keys](https://console.cloud.google.com/compute/metadata/sshKeys)
- Every instance launched in your project will be accessible via the users/keys you setup here
- For even finer control of the Google Cloud offerings, consider downloading their `gcloud` tool ([MacOS](https://cloud.google.com/sdk/docs/quickstart-macos))
- Then you can run cmds like:
```
gcloud auth login
gcloud config set project <your projectID>
gcloud compute instances list
gcloud compute instances describe <your instance name> --format json
```

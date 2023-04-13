# Aim on Spaces

Exciting news! We're delighted to announce the addition of Aim on Hugging Face Spaces. With just a few clicks, you can now easily deploy Aim on the Hugging Face Hub! 🚀

Aim is an open-source, self-hosted AI Metadata tracking tool designed to handle 100,000s of tracked metadata sequences. Two most famous AI metadata applications are: experiment tracking and prompt engineering. To uncover the full potential of Aim, please refer to the [GitHub repository](https://github.com/aimhubio/aim).

## Deploy Aim on Spaces

Starting with Aim on Spaces has never been simpler! To create a new space on Hugging Face, begin by clicking the dropdown menu located in the top right corner of the homepage that displays your profile. Next, select the option '+ New Space'. Upon clicking, you'll be redirected to the 'Create a new Space' page where you'll be required to fill out the fields as shown in the screenshot:

<img src="https://user-images.githubusercontent.com/23078323/231592155-869148a0-9a92-475f-8ebe-34d4deb2abc2.png" alt="Creating an Aim Space" width=800 />

After creating the space, you'll be able to monitor its progress through the Building status. Once it transitions to Running, your space is good to go!”

Upon navigating to the App section of your space, you can use Aim just as you would normally. By utilizing Aim, you (and anyone else who has access to the space) can view comprehensive logs of model training, allowing for a better understanding of the model being used.

This setup offers a fantastic feature wherein generating a new set of logs only requires committing the changes to the repository. HF Spaces will then automatically deploy the repository, making the process incredibly convenient. Isn't that great? ☺️

## Quick Start: Aim on HF Spaces end-to-end example

### Start with Aim

We can showcase a straightforward fine-tuning setup using Aim on Spaces. To achieve this, we simply need to follow the steps outlined in the Transformers tutorials, available at [Transformers page](https://huggingface.co/docs/transformers/training).

Aim is seamlessly integrated with HuggingFace Transformers. To use Aim with Transformers, simply include the appropriate AimCallback in your training arguments and let Aim handle the rest. Here's a code snippet demonstrating this integration:

```python
from aim.hugging_face import AimCallback

aim_callback = AimCallback(repo='your_repo_path', experiment='your_experiment_name')

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=small_train_dataset,
    eval_dataset=small_eval_dataset,
    compute_metrics=compute_metrics,
    callbacks=[aim_callback]
)
```

The AimCallback will automatically create an Aim Run and close it when the training is finished. When you perform an action on the trainer such as train, evaluate, or predict, the aim_callback will automatically log the hyperparameters and respective metrics.

The tutorial uses the 'yelp_review_full' dataset to fine-tune the pre-trained 'bert-base-cased' model. To broaden the tutorial's focus, we can experiment with two additional pre-trained models, such as 'xlm-roberta-base' and 'roberta-base'.

You can also find a more detailed example of fine-tuning Transformers models on the GLUE benchmark [here](https://github.com/aimhubio/aim/blob/main/examples/hugging_face_track.py). If you're interested in learning more about Aim and Aim with Transformers, you can check out this [blogpost](https://medium.com/aimstack/aim-v2-2-0-hugging-face-integration-57efa2eec104) which provides a detailed guide on using Aim with Transformers.

### Running Aim on HF spaces

When the experiments are tracked using Aim, the logs are saved in an .aim directory. To view the logs with Aim in your HF space, you need to compress this folder into an aim_repo.tar.gz file, with the following command:

```bash
tar -czvf aim_repo.tar.gz .aim
```

After which upload the compressed file to your space using git or the ‘Files and Versions’ section.

Please keep in mind that in this example, we've used aim_repo as the name of the .tar.gz file. However, you have the flexibility to give the compressed file any name you wish and then rename it in the Dockerfile. Don’t forget to push your changes. ☺️

That's it! After completing the previous steps, when you navigate to the ‘App’ section of your space, you'll see the Aim interface displaying your logs. 💫

<!-- TODO add a screenshot of Main Explorer page -->

### Exploring the runs with Aim

Aim provides a performant and beautiful UI for exploring and comparing training runs, prompt sessions. Additionally, its SDK enables programmatic access to tracked metadata — perfect for automations and Jupyter Notebook analysis.

The 'Metrics Explorer' page is where you will likely spend most of your time exploring the progress and results of your runs. On the 'Metrics Explorer' page, you can choose which metrics you want to track and use Aim's 'Pythonic search' functionality to easily filter your runs based on metrics and hyperparameters. This allows for much more in-depth demos of model experiments. Aim offers many other features as well, so be sure to check out [the documentation](https://aimstack.readthedocs.io/en/latest/overview.html) to explore its full potential.

<!-- TODO add a screenshot of Metrics Explorer page -->

If you want to delve deeper into Hugging face Aim Spaces and play around with the Aim UI, check out the [demo spaces](https://huggingface.co/aimstack) we have on the Hugging face Hub.

## Feedback and support

If you need support or have any improvement suggestions, please join the [Aim community on GitHub](https://github.com/aimhubio). 🤗

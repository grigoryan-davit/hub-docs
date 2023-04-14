# Aim on Spaces

**Aim** is an easy-to-use & supercharged open-source experiment tracker. Aim logs your training runs and enables a beautiful UI to compare them and an API to query them programmatically.
ML engineers and researchers use Aim explorers to compare 1000s of training runs in a few clicks.

Check out the [Aim docs](https://aimstack.readthedocs.io/en/latest/) to learn more about Aim.
If you have an idea for a new feature or have noticed a bug, feel free to [open a feature request or report a bug](https://github.com/aimhubio/aim/issues/new/choose).

In the following sections, you'll learn how to deploy Aim on the Hugging Face Hub Spaces and explore your training runs directly from the Hub.

## Deploy Aim on Spaces

You can deploy Aim on Spaces with just a few clicks:

<a  href="https://huggingface.co/new-space?template=aimstack/text2speech">
    <img src="https://huggingface.co/datasets/huggingface/badges/raw/main/deploy-to-spaces-lg.svg" />
</a>

<!-- TODO right link -->
All you need to do is:

1. Define the owner (your personal account or organization)
2. Name your Space
3. Choose the **Aim** Docker template
4. Set the visibility

Once you have created the Space, you'll see the `Building` status, and once it becomes `Running,` your Space is ready to go!

<img src="https://user-images.githubusercontent.com/23078323/231592155-869148a0-9a92-475f-8ebe-34d4deb2abc2.png" alt="Creating an Aim Space" width=800 />

Now, when you navigate to your Space's **App** section, you can access the Aim UI.

## Compare your experiments with Aim on Spaces

Let's use a quick example of a PyTorch CNN trained on MNIST to demonstrate end-to-end Aim on Spaces deployment.
The full example is in the [Aim repo examples folder](https://github.com/aimhubio/aim/blob/main/examples/pytorch_track.py).

```python
from aim import Run
from aim.pytorch import track_gradients_dists, track_params_dists

# Initialize a new Run
aim_run = Run()
...
items = {'accuracy': acc, 'loss': loss}
aim_run.track(items, epoch=epoch, context={'subset': 'train'})

# Track weights and gradients distributions
track_params_dists(model, aim_run)
track_gradients_dists(model, aim_run)
```

The experiments tracked by Aim are stored in the `.aim` folder. **To display the logs with the Aim UI in your Space, you need to compress the `.aim` folder to a `tar.gz` file and upload it to your Space using `git` or the Files and Versions sections of your Space.**

Here's a bash command for that:

```bash
tar -czvf aim_repo.tar.gz .aim
```

That’s it! Now open the App section of your Space and the Aim UI is available with your logs.
Here is what to expect:

![Aim UI on HF Hub Spaces](https://user-images.githubusercontent.com/67782184/224995208-692afbea-dfe0-4d2a-89ac-4ba552e49a98.png)

Filter your runs using Aim’s Pythonic search. You can write pythonic [queries against](https://aimstack.readthedocs.io/en/latest/using/search.html) EVERYTHING you have tracked - metrics, hyperparams etc.

<!-- TODO change image -->
![image](https://user-images.githubusercontent.com/67782184/224995427-db0d8a2b-1d48-46d1-b519-78a2d4d5d0aa.png)

Check out a [text2speech example ](https://huggingface.co/spaces/aimstack/text2speech/tree/main) on HF Hub Spaces.

<Tip>
If your logs are in TensorBoard format, you can easily convert [them to Aim with one command](https://aimstack.readthedocs.io/en/latest/quick_start/convert_data.html#show-tensorboard-logs-in-aim) and use the many advanced and high-performant training run comparison features available.
</Tip>

## More on HF Spaces

<<<<<<< HEAD
- [HF Docker spaces](https://github.com/huggingface/hub-docs/blob/main/docs/hub/spaces-sdks-docker.md)
- [HF Docker space examples](https://github.com/huggingface/hub-docs/blob/main/docs/hub/spaces-sdks-docker.md)
=======
<img width="1440" alt="Metrics Explorer" src="https://user-images.githubusercontent.com/23078323/231906739-ae1017cc-3d5f-4e75-af3d-0ca29f40ee14.png">

>>>>>>> 873615be0a29acda599db67702139cafe450c851

## Feedback and Support

If you have improvement suggestions or need support, please open an issue on [Aim GitHub repo](https://github.com/aimhubio/aim).

The [Aim community Discord](https://github.com/aimhubio/aim#-community) is also available for community discussions.

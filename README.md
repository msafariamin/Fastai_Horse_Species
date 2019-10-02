# Fastai_Horse_Species

I'm going to try to create a species horses detector. And I'm going to separate each species horses.  


Step 1: Gather URLs of each class of images

Our starting point is to find some pictures of species horses so we can learn what they look like. So I go to https://images.google.com/ and I type in Arabe horses for example and I just scroll through until I find a goodly bunch of them.

Then I go back to the notebook and you can see it says "go to Google Images and search and scroll." The next thing we need to do is to get a list of all the URLs there. To do that, back in your google images, open JavaScript Console in Develop on mac, and you paste the following into the window that appears:

```
#javascript:document.body.innerHTML = `<a href="data:text/csv;charset=utf-8,${escape(Array.from(document.querySelectorAll('.rg_di .rg_meta')).map(el=>JSON.parse(el.textContent).ou).join('\n'))}" download="links.txt">download urls</a>`;
```

This is a Javascript console for those of you who haven't done any Javascript before. I hit enter and it downloads my file for me. So I would call this urls_Arabe.txt and press "Save". Okay, now I have a file containing URLs of teddies. Then I would repeat that process for other species that I want, and I put each one in a file with an appropriate name.


Step 2: Download images

So step 2 is we now need to download those URLs to our server. Because remember when we're using Jupyter Notebook, it's not running on our computer. It's running on Google cloud (for me). So to do that, we start running some Jupyer cells. Let's grab the fastai library.(you can see it in my jupyter file)

And let's start with Arabe horse. So I click on this cell for Arabe horse and I'll run it. I've got six different cells doing the same thing but different information. This is one way I like to work with Jupyter notebook. I click on the Arabe horse cell, and run it to create a folder called Arabe and a file called urls_Arabe.txt for my Arabe horse. I skip the next five cells.

Then I go down to the next section and I run the next cell which is download images for Arabe horse. So that's just going to download my Arabe horse to that folder.

Now I go back and I click on 'horses'. And I scroll back down and repeat the same thing. That way, I'm just going backwards and forwards to download each of the classes that I want. 
So that will download the images to your server. It's going to use multiple processes to do so. 

Step 3: Create ImageDataBunch

The next thing that I found I needed to do was to remove the images that aren't actually images at all. This happens all the time. There's always a few images in every batch that are corrupted for whatever reason. Google image told us this URL had an image but it doesn't anymore. So we got this thing in the library called verify_images which will check all of the images in a path and will tell you if there's a problem. If you say delete=True, it will actually delete it for you. So that's a really nice easy way to end up with a clean dataset.
So at this point, I now have a bears folder containing a grizzly folder, teddys folder, and black folder. In other words, I have the basic structure we need to create an ImageDataBunch to start doing some deep learning. So let's go ahead and do that.

Now, very often, when you download a dataset from like Kaggle or from some academic dataset, there will often be folders called train, valid, and test containing the different datasets. In this case, we don't have a separate validation set because we just grabbed these images from Google search. But you still need a validation set, otherwise you don't know how well your model is going and we'll talk more about this in a moment.

Whenever you create a data bunch, if you don't have a separate training and validation set, then you can just say the training set is in the current folder (i.e. . because by default, it looks in a folder called train). So this is going to create a validation set for you automatically and randomly. You'll see that whenever I create a validation set randomly, I always set my random seed to something fixed beforehand. This means that every time I run this code, I'll get the same validation set. The randomness is a really important part of finding out your is solution stable and it is going to work each time you run it. But what is important is that you always have the same validation set. Otherwise when you are trying to decide has this hyper parameter change improved my model but you've got a different set of data you are testing it on, then you don't know maybe that set of data just happens to be a bit easier. So that's why I always set the random seed here.

Step 4: Training a model

So at that point, we can go ahead and create our convolutional neural network using that data. I tend to default to using a resnet34, and let's print out the error rate each time.

As per usual, we can use the ClassificationInterpretation class to have a look at what's going on. But we have some mistake. There was some species classified as someother. So we have to try to minimise the errors by the methode of cleaning.






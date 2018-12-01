# GCP_Install and Setting

https://cloud.google.com

Dear Zubair.


Access the above link and receive $300 credit

Make Project

![대체 텍스트](/figure/1-1.png)

![대체 텍스트](/figure/2-1.PNG)


Click on the **navigation menu** (bright green circle) in the upper left corner
and enter **ML Engine** to create the **model**.


As shown in the picture above, it is good to leave that services fixed.



![대체 텍스트](/figure/10.png)



Enter **storage** , **Browser** and **CREATE BUCKET**.

> Naming, Multi-Regional for default storage class , and Asia for Location.


***

https://console.cloud.google.com/flows/enableapi?apiid=ml.googleapis.com,compute_component&_ga=2.109735046.-2023158229.1525695083


Enter the above link to register the project.


Like this.


![대체 텍스트](/figure/4.png)


> If dosen't work, enter  https://cloud.google.com/ml-engine/docs/tensorflow/getting-started-training-prediction
>
> that link is official tutorial, and you can find **Enable the Cloud Machine Learning Engine and Compute Engine APIs**.
>
> hit the **ENABLE THE APIS** button.




***


https://console.cloud.google.com/apis/credentials/serviceaccountkey?_ga=2.104613379.-2023158229.1525695083



Enter the above link to create a service account key

Choose **Compute Engine default service account**

> Now you know what to do when dosen't work.
>
> Go to the Google official tutorial, and find **Go to the Create service account key page in the GCP Console.**
> 
> and hit the **Go to the Create service account key page** button.


![대체 텍스트](/figure/5.png)


If you can see this scene, you are doing the right thing.


Select **JSON** for key type.


Then, you can see JSON file is download.


![대체 텍스트](/figure/6.png)


I mkdir and move that file like dis.


***

Open CMD, and hit the command below.



For PATH, enter the location of the JSON file that you just downloaded.


We setting window environment.



**set GOOGLE_APPLICATION_CREDENTIALS=[PATH]**


This is my case.


**set GOOGLE_APPLICATION_CREDENTIALS=[C:\Users\SDH\Desktop\MINESLAB\GCP_tensorflow_test\test-f0439c5d022a.json]**


You done all? Then click on the link below to download Google Cloud SDK.


https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe


If installed, run CMD.

and hit **gcloud init** . This is initializing google cloud.


All you have to do is do yourself, except the area.


There were several counties that dosen't work with 09/28/2018.


Shell will let you know what is disable. So, you can choose avoid that region.



***

If you did init, move your step to blow.

Get on the Google Cloud platform and go to your own project.



![대체 텍스트](/figure/7.png)



At the point, copy your project ID.


ageless bla bla, dis is in my case.


![대체 텍스트](/figure/1-1.png)


In the upper right menu, there is a **activation Cloud Shell** (yellowish circle)button.

Hit that button, and when console is run, type blow command.


**gcloud config set project [selected-project-id]**

Paste the project ID of the project you copied in the bracket.

Make sure don't typing bracket, or you can meet blow error.


![대체 텍스트](/figure/8.png)



***

If you done above process, open CMD, and put blow command.


**gcloud ml-engine models list**


![대체 텍스트](/figure/9.png)


If you can see dis scene, you such a pro.


**gcloud projects list** allows you to view all projects in your account.

Other commands can be viewed by typing **gCloud --help**.


***

Make python file named **__init__.py**. Two underlines should be attached to the front and back.

> The grammar of the github Markdown does not show the underbar. 
> There must be a way, but I don't know how.
> WHAT A NICE!
> See the picture below.

It doesn't matter if empty file.


Then, they do simple coding.


I made a simple calculation.


![대체 텍스트](/figure/11.png)


And save somewhere.


***

Open CMD, and write long long command.


![대체 텍스트](/figure/12.png)



**gcloud ml-engine jobs submit training** [job name] **--package-path=** [upper path of your source] 

**--module-name=** [upper path of your source and name] 

**--staging-bucket=**[gs:// your bucket name you make]

This is one line.


Life is short, and art is long, but your command is longer.


Type that bunch of the command and run, you might see **state:QUEUED**.

If you nod your head at this point, you are pro.

And you may see this when you access Google Cloud Platform, ML Engine.

The picture with the above gcloud command also shows on the upper line of state:QUEUED.



![대체 텍스트](/figure/13.png)


You want to see the progress of the task in the cmd window, you can enter the command below.




![대체 텍스트](/figure/14.png)




**gcloud ml-engine jobs stream-logs** [job name]



***



![대체 텍스트](/figure/15.png)



If the work is done, the results will come out as above.


You can check your payment information by going to **Billing** in the navigation menu.


You can also check the expiration date and balance of the 300$ credits you signed up for.



***USE GPU & Choose Runtime Version, Python Version


Now let's find out how to use GPU, most of the reasons why we use ml engine.


ml engine provides a variety of high-performance computing machines such as CPU and TPU as well as GPU.


Let's add a TPU later and find out how to use GPU this time.


First, below are the types and prices of predefined GPU machines provided by ml engine.


The standard for price measurement is Asia Pacific.


![대체 텍스트](/figure/gpu.png)


**BASIC**과 **STANDARD_1, PREMIUM_1** is CPU machine.


**BASIC_GPU** is the machine that can use **NVIDIA Tesla K80**.


In other words, we can use the K80 GPU for about $1.36 per hour.


You can also use multiple K80 GPUs or **NVIDIA Tesla P100**, **NVIDIA Tesla V100**.


but not today, we use single k80.


***


**gcloud ml-engine ...**


![대체 텍스트](/figure/12.png)


Maybe you already know,  the order to follow  **--** is similar to an option.


Write down **--scale-tier=basic_gpu** after which GPU usage setting is complete.


You will see the following command if you order it to be executed.



![대체 텍스트](/figure/gpu2.png)


***


Now, we will choose **runtime version** and  **Python version**.


https://cloud.google.com/ml-engine/docs/tensorflow/runtime-version-list


The above links show the runtime version of ml engine, 

supported packages according to version, and the Python version.


As of Nov 10, 2018, the latest version is Version 1.10,

If the option is not set, it runs as a 1.0 version with default values.


For Python 3.5, operation is only possible with version 1.4 or higher.

Also, bcuz the version of the tensorflow varies depending on the runtime version, choose the version you need.


Like the above compute-machine selection(GPU), **--** is attached to set the runtime version.

In my case, add option with using python 3


**gcloud ml-engine jobs submit test_bundle --package-path=./ --module-name=test.test --staging-bucket=gs://sdh-satellite --scale-tier=basic_gpu --python-version=3.5 --runtime-version=1.10**


So if you will write it down, you will be using GPUs, Python 3.5,
and packages that supported by ml engine 1.10.


If you already done the basic tutorial above, 
you know **gcloud ml-engine jobs describe job-name** command.

Not stream-logs, it's jobs description.


Run the **jobs describe** command. you can see description of your job.

Like this.


![대체 텍스트](/figure/jobs_descr.png)

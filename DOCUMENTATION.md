<h1>Welcome to Intellead Data documentation!</h1>
Intellead Data aims to be an easy way to store and retrieval data of leads for Intellead project.

<h3>Contents</h3>
<ul>
  <li>Introduction</li>
    <ul>
      <li>Features</li>
    </ul>
  <li>Instalation
    <ul>
      <li>Dependencies</li>
      <li>Get a copy</li>
    </ul>
  </li>
  <li>Configuration
  <ul>
    <li>Receiving data</li>
    <li>Persisting data</li>
  </li>
  <li>Use Cases
    <ul>
      <li>Receive RDStation data</li>
      <li>Return data for all leads</li>
      <li>Return data from a specific lead</li>
      <li>Update lead data with enrichment</li>
    </ul>
  </li>
  <li>Copyrights and Licence</li>
</ul>
<h3>Introduction</h3>
Intellead Data aims to be an easy way to store and retrieval data for Intellead environment supporting by http protocol.
<h4>Features</h4>
This application provides lead registration, lead update and lead retrieval.
<h3>Instalation</h3>
intellead-data is a very smaller component that provide a simple way to receive data, store and retrieval.
This way you do not need to install any other components for this to work.
<h4>Dependencies</h4>
Despite what has been said above, today this application receives data from RDStation through a webhook made available by Digital Results. That way you need to use RDStation and configure a webhook to receive the data.
In the configuration section, we'll talk a bit more about this.
<h4>Get a copy</h4>
I like to encourage you to contribute to the repository.<br>
This should be as easy as possible for you but there are few things to consider when contributing. The following guidelines for contribution should be followed if you want to submit a pull request.
<ul>
  <li>You need a GitHub account</li>
  <li>Submit an issue ticket for your issue if there is no one yet.</li>
  <li>If you are able and want to fix this, fork the repository on GitHub</li>
  <li>Make commits of logical units and describe them properly.</li>
  <li>If possible, submit tests to your patch / new feature so it can be tested easily.</li>
  <li>Assure nothing is broken by running all the tests.</li>
  <li>Open a pull request to the original repository and choose the right original branch you want to patch.</li>
  <li>Even if you have write access to the repository, do not directly push or merge pull-requests. Let another team member review your pull request and approve.</li>
</ul>
<h3>Configuration</h3>
Once the application is installed (check Installation) define the following settings to enable the application behavior. 
<h4>Receiving data</h4>
Today the application receives the RDStation data through a webhook.
The first configuration to do is to create the webhook through the RDStation Integrations menu.
You must:
<ul>
  <li>set the name of the webhook;</li>
  <li>To url: https: www.your_host.com<b>/rd-webhook</b>;</li>
  <li>The trigger and,</li>
  <li>Conversion events.</li>
</ul>
<h4>Persisting data</h4>
You must config var <b>MONGODB_URI</b> to persist data.
<h3>Use Cases</h3>
Some use cases for intellead-data.
<h4>Receive RDStation data</h4>
RDStation provides a webhook to send us data of the lead.
Once we have configured the webhook in RDStation, the service will be available to receive the data.
<h4>Return data for all leads</h4>
In some cases, you might need to retrieve all data from all leads.
As there may be a lot of information, this service proves paginated data. That way you need to inform the number of leads you want and the number of the page.
We can call the API like this:

```javascript
var page = $('#page_number').val();
var size = $('#page_size').val();
$.ajax({
    "crossDomain": true,
    "url": "https://your_domain.com/all-leads",
    "method": "POST",
    "headers": {
        "content-type": "application/x-www-form-urlencoded",
        "cache-control": "no-cache"
    },
    "data": {
        page_number : page,
        page_size : size
    },
})
```

<h4>Return data from a specific lead</h4>
Sometimes it’s desirable that retrieve all data from a specific lead.
You just need to inform the id of the lead.
We can call API like this:

```javascript
var id = $('#lead_id').val();
$.ajax({
    "crossDomain": true,
    "url": "https://your_domain.com/lead-info",
    "method": "POST",
    "headers": {
        "content-type": "application/x-www-form-urlencoded",
        "cache-control": "no-cache"
    },
    "data": {
        lead_id : id
    },
});

```

<h4>Update lead data with enrichment</h4>
When the lead information is enriched, this service proves a way to update the data in the database.
We can call the API like this:

```javascript
var lead_enriched = JSON.parse(data);
request.post(
    'https://your_domain.com/update-enriched-lead-information',
    { 
        json: { 
            lead_id: id, 
            rich_information: lead_enriched 
        } 
    },
    function (error, response, body) {
        if (error) {
            console.log(error);
        }
    }
);
```

Used by the intellead-enrich service.
<h3>Copyrights and Licence</h3>
TO DO
# Actor - Allrecipes Advanced Scraper

## Allrecipes Advanced scraper

Since Allrecipes doesn't provide a good and free API, this actor should help you to retrieve data from it. This actor can provide you very detailed

The Allrecipes Advanced data scraper supports the following features:

-   Search any keyword or ingredient - You can search any keyword you would like to have and get the results.

-   Include or exclude any ingredient - You can include or exclude some keywords from the search results.

-   Scrape recipes - Scrape any recipes in a very detailed and structured from Allrecipes.

-   Scrape articles - Fetch any articles that has been published from Allrecipes.

-   Scrape galleries - You can scrape any gallery that you need. It is structured and provides all the slides.

-   Scrape authors and users - If you want to scrape the data of a specific author or user, you can just provide it and Allrecipes Advanced scraper will do the rest.

-   Scrape collections - You can scrape user-generated collections and all of its recipes.

## What are the advantages of this actor compared to others?
This actor is extremely optimized, very fast and provides at least 5x more data than the other actors or projects that you might experienced. Also, it is actively maintained so if you need any kind of features, you can inform me from [here](https://github.com/tugkan/allrecipes-advanced-scraper/issues) and I can make it for free.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/tugkan/allrecipes-advanced-scraper/issues).

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Allrecipes that should be visited. Required fields are:

| Field                | Type    | Description                                                                                                                                                                                                    |
| -------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| search               | String  | (optional) Keyword that you want to search on Allrecipes.                                                                                                                                                       |
| includedKeywords               | Array  | (optional) Ingredients or keywords that you want to include.                                                                                                                                                       |
| excludedKeywords               | Array  | (optional) Ingredients or keywords that you want to exclude.                                                                                                                                                       |
| startUrls            | Array   | (optional) List of Allrecipes URLs. You should only provide recipe list, search, author, user, recipe detail, collection, gallery and article URLs                                                                                                                 |
| endPage              | Integer | (optional) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.                                                          |
| maxItems             | Integer | (optional) You can limit scraped items. This should be useful when you search through the big subcategories.                                                                                                |
| proxy                | Object  | Proxy configuration                                                                                                                                                                                            |
| extendOutputFunction | String  | (optional) Function that takes a JQuery handle ($) as argument and returns object with data                                                                                                                    |
| customMapFunction | String  | (optional) Function that takes each objects handle as argument and returns object with executing the function                                                                                                                     |

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

##### Tip

When you want to have a scrape over a specific item URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape many as items as possible. Therefore, it forefronts all item detail requests. If actor doesn't block very often it'll scrape 100 items in 1 minute with ~0.01-0.04 compute units.

### Allrecipes Advanced Scraper Input example

```json
{
  "startUrls":[
    "https://www.allrecipes.com/cook/onewholesomemeal",
    "https://www.allrecipes.com/cook/foodwisheswithchefjohn/collection/bookmarks_5e9f2dfb-c75b-8640-f3ff-7897a9ed3897",
    "https://www.allrecipes.com/search/results/?search=cucumber",
    "https://www.allrecipes.com/gallery/butter-rich-recipes/",
    "https://www.allrecipes.com/author/melanie-fincher/",
    "https://www.allrecipes.com/article/how-to-clean-air-fryer/",
    "https://www.allrecipes.com/recipe/261911/chef-johns-croissants/"
  ],
  "proxy":{
    "useApifyProxy": true
  },
  "search": "cucumber",
  "includedKeywords":["salad"],
  "excludedKeywords":["onion"],
  "maxItems": 50,
  "endPage": 20
}

```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## Allrecipes Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Allrecipes Advanced actor.

## Scraped Allrecipes Output

The structure of each item in Allrecipes looks like this:

### Recipe Detail

```json
{
  "url": "https://www.allrecipes.com/recipe/261911/chef-johns-croissants/",
  "name": "Chef John's Croissants",
  "breadcrumbs": [
    "Bread",
    "Yeast Bread Recipes"
  ],
  "rating": "4.5",
  "summary": "I wouldn't describe making homemade croissants as easy since there are multiple steps, and it does take at least half a day. But it's really not that hard either; and certainly simpler than flying to Paris, which is the only other way to enjoy these amazing pastries. This recipe was adapted from one by Bruno Albouze, from The Real Deal (which he is).",
  "reviews": "",
  "photos": [
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2020%2F02%2FMorel-Mushrooms-by-Kevin-Miyazaki-2000.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2014%2F12%2F395820-Rhubarb-and-Strawberry-Pie-Photo-by-CookinBug-650x465.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2020%2F04%2F27%2Fraspberry-almond-coffeecake.jpeg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2020%2F02%2Fcreamy-strawberry-crepes.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2020%2F12%2F16%2F8792389_korean-street-toast_chef-john-2000.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2022%2F04%2F07%2FSalad-Ingredients-2000.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2019%2F12%2F5205125.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2021%2F07%2F21%2F151075-herb-buttermilk-biscuits-naples34102.jpeg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2020%2F02%2F4511165-2000.jpg",
    "/img/icons/generic-recipe.svg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2020%2F07%2F27%2FScreen-Shot-2020-07-27-at-10.42.25-AM.png",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2022%2F04%2F01%2FGettyImages-677135427-2000.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2022%2F03%2F09%2F81108-classic-macaroni-salad-mfs-034.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2020%2F07%2F31%2FLemon-Chicken-Orzo-Soup.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2022%2F03%2F22%2F3022266-saltine-toffee-cookies-photo-by-sporkism.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2022%2F01%2F13%2FGettyImages-1249377035.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2021%2F02%2F24%2F280504-mediterranean-orzo-salad-kims-cooking-now-2000.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2021%2F05%2F20%2F102189514_korean-barbecue-with-bachan_allrecipes-2000.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2022%2F03%2F22%2Fhow-to-host-your-first-dinner-party-2x1-102709103.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2022%2F01%2F20%2FGettyImages-1358089502-2000.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F9135335.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F9011803.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F8765419.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F8732830.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F4674617.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fmobile%2Fallrecipes%2Fimages%2Ficon-user-default_v2.png",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F5499721.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6143666.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6036163.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F7826687.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6864562.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6497561.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F5311132.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F7496757.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6966693.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F8076003.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6751311.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F8031258.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6571769.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F5202780.jpg",
    "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fwww.allrecipes.com%2Fimg%2Fmisc%2F300x250_magazines_and_more.jpg"
  ],
  "author": {
    "name": ""
  },
  "cook": "25 mins",
  "additional": "3 hrs",
  "total": "3 hrs 55 mins",
  "prep": "30 mins",
  "Servings": "8",
  "Yield": "12 to 16 croissants",
  "ingredients": [
    "1 cup warm water (100 degrees F or 38 degrees C)",
    "1 (.25 ounce) package active dry yeast",
    "¼ cup granulated white sugar",
    "3 ½ cups unbleached bread flour",
    "3 teaspoons kosher salt",
    "6 tablespoons butter, room temperature, cut into pieces",
    "2 sticks unsalted European-style butter",
    "1 egg",
    "1 tablespoon water"
  ],
  "directions": [
    {
      "name": "Step 1",
      "description": "Place warm water in the bowl of a stand mixer. Sprinkle with yeast. Let yeast dissolve for 10 minutes. Add sugar and bread flour. Sprinkle with salt; add 6 tablespoons butter. Attach the bowl to the stand mixer. Mix dough with the dough hook just until butter is completely kneaded in and the dough forms a ball and pulls away cleanly from the sides of the bowl, 3 or 4 minutes."
    },
    {
      "name": "Step 2",
      "description": "Transfer dough to a work surface and form into a semi-smooth ball. Place dough back in the mixer bowl; cover. Let rise in a warm spot until doubled, about 2 hours."
    },
    {
      "name": "Step 3",
      "description": "Transfer dough to a lightly floured work surface. Push and press dough to deflate it, and form it into a rectangle. Fold into thirds by lifting one end over the middle third, and folding the other side onto the middle. Wrap in plastic wrap. Place on a rimmed baking sheet lined with a silicone mat. Refrigerate until chilled through, about 1 hour."
    },
    {
      "name": "Step 4",
      "description": "Cut 2 sticks butter in half lengthwise and place slightly apart from each other on a length of parchment paper long enough to fold over the butter. Fold the parchment paper over the butter. Press butter down. Roll out with a rolling pin to a square about 8x8 inches. Refrigerate until a little chilled and just barely flexible, 10 or 15 minutes."
    },
    {
      "name": "Step 5",
      "description": "Roll dough out into a rectangle slightly wider than the butter slab and just over twice as long. Place butter on one half of the dough leaving about 1 inch margin from the edge of the dough. Fold the other half of the dough over the butter. Dust work surface and dough with flour as needed."
    },
    {
      "name": "Step 6",
      "description": "Press rolling pin down on dough to create ridges. Then roll out the ridges. Repeat this process. Keep pressing and rolling until dough is about the same size rectangle as you had before you folded it in half, dusting with just a bit of flour as necessary."
    },
    {
      "name": "Step 7",
      "description": "Starting from the short side, fold one-third of dough over middle third. Then fold the other end over to form a small rectangle. Flatten out just slightly with rolling pin. Transfer to the silicone-lined baking sheet; cover with plastic wrap. Refrigerate until chilled, about 30 minutes."
    },
    {
      "name": "Step 8",
      "description": "Transfer dough back to work surface and repeat pressing and rolling technique until dough is the size of the previous larger rectangle. Fold into thirds again, starting from the short side. Press and roll slightly. Transfer back to lined baking sheet. Cover and refrigerate about 15 minutes."
    },
    {
      "name": "Step 9",
      "description": "Roll back out to a large rectangle. This time, fold dough in half. Then press and roll out into a 1/2-inch thick rectangle, using as little flour as needed to keep dough from sticking."
    },
    {
      "name": "Step 10",
      "description": "Cut dough in half lengthwise using a pastry wheel or pizza cutter. Dust one piece with flour and roll out to a rectangle about 1/4 to 1/8 inch thick. Starting from one corner, cut the dough diagonally crosswise into 8 triangles using a pastry wheel. Starting with the bottom end of each triangle, roll each up toward the tip to form the croissant with the seam at the bottom. If necessary, use a bit of water to seal the tip to the rolled croissant."
    },
    {
      "name": "Step 11",
      "description": "Repeat with the other half of the dough."
    },
    {
      "name": "Step 12",
      "description": "Place shaped croissants on baking sheets lined with silicone mats. Whisk together egg and 1 tablespoon water to make the egg wash. Brush croissants with egg wash. Place in a warm area to allow them to rise, about 45 to 60 minutes."
    },
    {
      "name": "Step 13",
      "description": "Preheat oven to 400 degrees F (200 degrees C). Brush croissants gently but thoroughly again with egg wash."
    },
    {
      "name": "Step 14",
      "description": "Bake in preheated oven until beautifully browned, about 25 minutes. Transfer to a cooling rack. Cool to room temperature before serving."
    }
  ],
  "nutritionFacts": [
    {
      "name": "protein",
      "value": "8.6g",
      "dailyValue": "17 %"
    },
    {
      "name": "carbohydrates",
      "value": "50.1g",
      "dailyValue": "16 %"
    },
    {
      "name": "dietary fiber",
      "value": "1.6g",
      "dailyValue": "7 %"
    },
    {
      "name": "sugars",
      "value": "6.5g",
      "dailyValue": ""
    },
    {
      "name": "fat",
      "value": "33.3g",
      "dailyValue": "51 %"
    },
    {
      "name": "saturated fat",
      "value": "20.4g",
      "dailyValue": "102 %"
    },
    {
      "name": "cholesterol",
      "value": "107.1mg",
      "dailyValue": "36 %"
    },
    {
      "name": "vitamin a iu",
      "value": "1006.3IU",
      "dailyValue": "20 %"
    },
    {
      "name": "niacin equivalents",
      "value": "6.6mg",
      "dailyValue": "51 %"
    },
    {
      "name": "folate",
      "value": "134.3mcg",
      "dailyValue": "34 %"
    },
    {
      "name": "calcium",
      "value": "23.2mg",
      "dailyValue": "2 %"
    },
    {
      "name": "iron",
      "value": "2.9mg",
      "dailyValue": "16 %"
    },
    {
      "name": "magnesium",
      "value": "17.7mg",
      "dailyValue": "6 %"
    },
    {
      "name": "potassium",
      "value": "95.6mg",
      "dailyValue": "3 %"
    },
    {
      "name": "sodium",
      "value": "795.8mg",
      "dailyValue": "32 %"
    },
    {
      "name": "thiamin",
      "value": "0.5mg",
      "dailyValue": "51 %"
    },
    {
      "name": "calories from fat",
      "value": "299.6",
      "dailyValue": ""
    }
  ]
}
```

### Article Item Detail

```json
{
  "url": "https://www.allrecipes.com/article/how-to-clean-air-fryer/",
  "title": "How to Clean Your Air Fryer",
  "breadcrumbs": [
    "Kitchen Tips",
    "How To",
    "Cleaning"
  ],
  "author": {
    "name": "Melanie Fincher",
    "url": "https://www.allrecipes.com/author/melanie-fincher/"
  },
  "date": "Updated April 29, 2022",
  "html": " <div class=\"partial lead-image align-default\"><div class=\"image-and-burst\"> <div class=\"component lazy-image lazy-image-udf undefined lead-media aspect_3x2 cache-only align-default\" data-src=\"https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2019%2F12%2FAir-Fryer-chicken-wings-2000.jpg\" data-use-imagesvc-to-cache=\"true\" data-special-crop=\"\" data-alt=\"Air Fryer Chicken Wings\" data-title=\"Air-Fryer-chicken-wings\" data-shop-image=\"false\" data-original-width=\"2000\" data-original-height=\"1333\" data-high-density=\"false\" data-crop-percentage=\"67\" data-tracking-zone=\"image\" data-orientation=\"default\"> <noscript><img src=\"https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2019%2F12%2FAir-Fryer-chicken-wings-2000.jpg\" alt=\"Air Fryer Chicken Wings\"></noscript> <div class=\"inner-container js-inner-container image-overlay\"> <span class=\"placeholderText visually-hidden\">Air Fryer Chicken Wings</span> <span class=\"icon icon-pinterest-circle-solid social-icon pinterest-transparent\" data-social-service=\"pinterest\"><a href=\"https://www.pinterest.com/pin/create/link/?url=https%3A%2F%2Fwww.allrecipes.com%2Farticle%2Fhow-to-clean-air-fryer%2F%3Futm_source%3Dpinterest.com%26utm_medium%3Dsocial%26utm_campaign%3Dsocial-share-article%26utm_content%3D20220506%26utm_term%3Dundefined&amp;media=https%3A%2F%2Fimagesvc.meredithcorp.io%2Fv3%2Fmm%2Fimage%3Furl%3Dhttps%253A%252F%252Fstatic.onecms.io%252Fwp-content%252Fuploads%252Fsites%252F43%252F2019%252F12%252FAir-Fryer-chicken-wings-2000.jpg&amp;description=How%20to%20Clean%20Your%20Air%20Fryer\" class=\"display-block allowPopup popup\" aria-label=\"Pin this Air Fryer Chicken Wings image\" title=\"pinterest share\"> <svg width=\"32\" height=\"32\" viewBox=\"0 0 32 32\" xmlns=\"http://www.w3.org/2000/svg\" aria-hidden=\"true\"><g fill=\"none\" fill-rule=\"evenodd\"><path d=\"M32 16c0 8.837-7.163 16-16 16S0 24.837 0 16 7.163 0 16 0s16 7.163 16 16\" fill=\"#E54A59\"></path><path d=\"M15.164 18.532c-.011.039-.022.072-.03.106-.503 1.97-.56 2.408-1.076 3.322-.246.436-.524.847-.832 1.242-.034.044-.067.102-.136.088-.076-.016-.082-.084-.09-.145-.083-.599-.128-1.2-.108-1.803.026-.788.123-1.058 1.139-5.327a.295.295 0 0 0-.024-.178c-.244-.656-.291-1.32-.079-1.995.459-1.456 2.11-1.567 2.398-.366.178.743-.292 1.716-.653 3.152-.299 1.186 1.097 2.03 2.29 1.163 1.1-.798 1.527-2.71 1.446-4.067-.16-2.703-3.125-3.287-5.005-2.417-2.157.997-2.647 3.67-1.673 4.891.123.156.219.25.177.408-.062.245-.117.49-.185.734-.05.182-.202.247-.385.173a2.212 2.212 0 0 1-.9-.675c-.827-1.024-1.064-3.049.03-4.763 1.21-1.9 3.463-2.668 5.52-2.435 2.457.28 4.01 1.958 4.3 3.863.133.867.038 3.006-1.18 4.518-1.402 1.737-3.672 1.852-4.72.786-.08-.082-.145-.178-.224-.275\" fill=\"#FFF\"></path></g></svg> </a></span> <button class=\"icon icon-image-zoom elementButton__defaultFocus\" data-image=\"https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2019%2F12%2FAir-Fryer-chicken-wings-2000.jpg\" data-caption=\"\" data-credit=\"Credit: Lauri Patterson/Getty Images\" data-alt=\"Air Fryer Chicken Wings\" data-title=\"Air-Fryer-chicken-wings\" aria-label=\"Make image larger Air-Fryer-chicken-wings\" data-tracking-do-not-track=\"1\"><svg xmlns=\"http://www.w3.org/2000/svg\" width=\"24\" height=\"24\" viewBox=\"0 0 24 24\"><path d=\"M2.667 21.333h8v2.667h-10.667v-10.667h2.667v8zM21.333 0h2.667v10.667h-2.667v-8h-8v-2.667h8z\"></path></svg> </button> </div><div class=\"lazy-image__loadingPlaceholder\"><img class=\"loadingPlaceholder\" alt=\"\" src=\"data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20100%2067'%3E%3C/svg%3E\" width=\"2000\" height=\"1333\"></div><div class=\"image-wrap-container clearfix\"><div class=\"credit body-credit padding-8-top padding-8-bottom elementFont__fine--credit\">Credit: Lauri Patterson/Getty Images</div></div></div></div></div>",
  "text": "<img src=\"https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2019%2F12%2FAir-Fryer-chicken-wings-2000.jpg\" alt=\"Air Fryer Chicken Wings\">  Air Fryer Chicken Wings      Credit: Lauri Patterson/Getty Images So you got an air fryer? If you've already put it to use, you know that these trendy kitchen gadgets allow you to still enjoy all your favorite fried foods with less fat and fewer calories. But you're still frying after all, which means you're going to have some grease to deal with afterward. The good news? It's an air fryer, so you're going to have way less greasy residue to clean than you would using a deep fryer. Learn how to clean your air fryer using items you likely already have on hand.    Tips for Cleaning Your Air Fryer  Before you deep clean your air fryer, learn the dos and don'ts of air fryer maintenance. Don't use metal utensils, abrasive sponges, or steel wire brushes to remove food particles and residue from your air fryer. This could damage the non-stick coating on the cooking surface.Don't submerge your air fryer in water. The main unit is an electric appliance, so this will damage it.Make sure your fryer is unplugged while you are cleaning.If you notice a foul odor coming from your air fryer, try cleaning the crevices with a wooden skewer, toothpick, or even an old toothbrush, to knock out stuck-on foods. These hidden crumbs can burn over time, causing the machine to smoke and smell.You can also cut half a lemon and rub the cooking surface and basket to help with residual odors. Let it sit for about 30 minutes before cleaning.Use food-safe cleaners. Avoid disinfectants that aren't approved for food contact.   How Often Should You Clean Your Air Fryer?   After Each Use  Each time you use your air fryer, wash the basket, tray, and pan with soap and warm water, or place them in the dishwasher. (Refer to the owner's manual to be sure these parts are dishwasher safe.) You should also quickly clean the interior using a damp cloth with a bit of dish soap over the area. Dry all the parts and reassemble.     After Every Few Uses  Though it's not necessary to take these steps after every use, washing the other main parts on occasion will keep your air fryer functioning properly. Use a damp cloth to wipe down the exterior every once in a while. You should also check the heating coil for oil or residue. If you notice some build-up there, wipe it with a damp cloth when the machine is cool.   How to Deep Clean an Air Fryer  If it's been a minute since you've given your air fryer a good clean, or you just don't know where to start, read on for our instructions on how to clean an air fryer from start to finish. Here's what you'll need:  Damp microfiber cloth or non-abrasive spongeDish soapBaking SodaSoft-bristle scrub brushClean, dry cloth Clean your air fryer by following a series of simple steps:  If you have just used it, start by unplugging your air fryer. Allow it to cool for about 30 minutes.Remove the baskets and pans, and wash with hot soapy water. If any of these parts have baked-on grease or food, allow the parts to soak in hot soapy water for at least 10 minutes before scrubbing with a non-abrasive sponge. Some of the parts may be dishwasher safe, so refer to your manual if you prefer to use the dishwasher to clean.Use a damp microfiber cloth or non-abrasive sponge with a bit of dish soap to wipe down the interior. Wipe away soap with a clean damp cloth.Turn the appliance upside down and use a damp cloth or sponge to wipe down the heating element.If there is any baked-on or hard residue on the main appliance, make a paste using water and baking soda. Scrub the paste into the residue using a soft-bristle scrub brush and wipe away with a clean cloth.Use a damp cloth to wipe down the exterior. Wipe away the soap with a clean damp cloth.Dry all removable parts and the main unit before reassembling. Related: Air Fryer Main Dishes for DinnerBest Holiday Party Appetizers to Make in the Air FryerBrowse our entire collection of Air Fryer Recipes."
}
```

### Gallery Item Detail

```json
{
  "url": "https://www.allrecipes.com/gallery/butter-rich-recipes/",
  "title": "50 of Our Most Buttery Recipes",
  "breadcrumbs": [
    "Ingredients",
    "Dairy Recipes",
    "Butter Recipes"
  ],
  "author": {
    "name": "Melanie FincherMelanie Fincher",
    "url": "https://www.allrecipes.com/author/melanie-fincher/"
  },
  "date": "March 01, 2022",
  "slides": [
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2021%2F03%2F12%2F401804.jpg",
      "title": "",
      "description": "We're firm believers that everything is better with butter, but don't take our word for it — these butter-rich recipes are all the proof you need. From gooey butter cakes to buttery roasted vegetables and more, check out our collection of recipes made better with butter."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F-0001%2F11%2F30%2F572806.jpg",
      "title": "Quick and Almost-Professional Buttercream Icing",
      "url": "https://www.allrecipes.com/recipe/174347/quick-and-almost-professional-buttercream-icing/",
      "description": "Use the highest quality butter you can get for this easy, bakery-quality buttercream — it makes all the difference."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2019%2F07%2F2432913.jpg",
      "title": "Buttery Garlic Green Beans",
      "url": "https://www.allrecipes.com/recipe/230103/buttery-garlic-green-beans/",
      "description": "This is a fail-proof way to dress up fresh greens beans using butter, garlic, and lemon pepper.  Reviewer Sarah Jo says, \"I usually double this recipe because my family inhales it.\""
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F2054794.jpg",
      "title": "Lemon-Buttermilk Pound Cake with Aunt Evelyn's Lemon Glaze",
      "url": "https://www.allrecipes.com/recipe/236915/lemon-buttermilk-pound-cake-with-aunt-evelyns-lemon-glaze/",
      "description": "Traditionally, pound cake is made with a pound of butter, pound of sugar, pound of eggs, and pound of flour. This updated version maintains the classic buttery flavor, but with the addition of lemon and buttermilk."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F-0001%2F11%2F30%2F2027161.jpg",
      "title": "Crab Legs with Garlic Butter Sauce",
      "url": "https://www.allrecipes.com/recipe/155375/crab-legs-with-garlic-butter-sauce/",
      "description": "Snow crab legs are simmered in a garlic-butter mixture — be sure to save the excess for dipping!"
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6918091.jpg",
      "title": "Grandma Rita's Soft Butter Rolls",
      "url": "https://www.allrecipes.com/recipe/237066/grandma-ritas-soft-butter-rolls/",
      "description": "\"Want a roll that stays soft for days? Try these fluffy, soft rolls made with butter and love,\" says recipe creator Lela. \"This is my Grandma's recipe. The rolls are quick to rise due to the two packages of yeast.\""
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F872252.jpg",
      "title": "Marshmallow Buttercream Frosting",
      "url": "https://www.allrecipes.com/recipe/222815/marshmallow-buttercream-frosting/",
      "description": "\"I admit that I was skeptical about a buttercream that uses SO MUCH butter and SO LITTLE powdered sugar!\" says reviewer Kim Carnahan. \"However, the marshmallow creme stirs in like a dream and adds a fluffiness that I've never see in a buttercream! This frosting melts in your mouth and the almond flavor is delectable.\""
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2021%2F11%2F04%2Fimage-30.jpg",
      "title": "Butter Swim Biscuits",
      "url": "https://www.allrecipes.com/recipe/280473/butter-swim-biscuits/",
      "description": "No need to butter these biscuits — they are baked in a pool of melted butter for an unbelievably buttery result."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F2518260.jpg",
      "title": "Buttered Noodles",
      "url": "https://www.allrecipes.com/recipe/244458/buttered-noodles/",
      "description": "This simple, budget-friendly recipe uses just three staple ingredients: fettuccine, butter, and Parmesan cheese."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F401804.jpg",
      "title": "Outrageously Buttery Crumb Cake",
      "url": "https://www.allrecipes.com/recipe/214562/outrageously-buttery-crumb-cake/",
      "description": "This ooey-gooey crumb cake uses a whopping one pound of butter for an ultra moist cake with a buttery crumb topping."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6505068.jpg",
      "title": "Baked Lemon-Butter Chicken Thighs",
      "url": "https://www.allrecipes.com/recipe/272544/baked-lemon-butter-chicken-thighs/",
      "description": "A lemon-butter sauce is used to baste these roasted chicken thighs. The resulting chicken is juicy on the inside with a crisp, flavorful skin."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F1351392.jpg",
      "title": "Ooey Gooey Butter Cake",
      "url": "https://www.allrecipes.com/recipe/236457/ooey-gooey-butter-cake/",
      "description": "This gooey butter cake features two layers: a buttery cake layer and a cream cheese filling layer. It's an unassuming cake served straight out of the pan, but don't be fooled by its looks — it's intensely sweet and yes, gooey."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F3274415.jpg",
      "title": "Italian Butterball Cookies",
      "url": "https://www.allrecipes.com/recipe/189046/italian-butterball-cookies/",
      "description": "These melt-in-your-mouth butter cookies are traditionally served during the holidays, but there's no reason you can't enjoy them year-round."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F2964818.jpg",
      "title": "Garlic Butter Acorn Squash",
      "url": "https://www.allrecipes.com/recipe/229736/garlic-butter-acorn-squash/",
      "description": "This recipe takes a more savory approach to sweet, nutty acorn squash."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F2400303.jpg",
      "title": "Chef John's Butter Puff Biscuit Dough",
      "url": "https://www.allrecipes.com/recipe/244473/chef-johns-butter-puff-biscuit-dough/",
      "description": "Chef John says this cross between puff pastry and biscuit dough works great for \"fruit tarts, ham and cheese turnovers, and chocolate croissants — and of course, plain biscuits served with butter and jam.\""
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F4483972.jpg",
      "title": "Kentucky Blue Ribbon All-Butter Pound Cake",
      "url": "https://www.allrecipes.com/recipe/257278/kentucky-blue-ribbon-all-butter-pound-cake/",
      "description": "This ribbon-winning pound cake has been in Taylor Piercefield's family for seven generations: \"Tastes like pure love!\""
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2021%2F11%2F12%2F9093941_original.jpg",
      "title": "Grandma's Creamy Peanut Butter Fudge",
      "url": "https://www.allrecipes.com/recipe/276663/grandmas-creamy-peanut-butter-fudge/",
      "description": "Butter and creamy-style peanut butter create a dense, old-fashioned fudge that melts in your mouth that moment it hits your tongue."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F4479865.jpg",
      "title": "Norwegian Butter Sauce (Sandefjordsmor)",
      "url": "https://www.allrecipes.com/recipe/257242/norwegian-butter-sauce-sandefjordsmor/",
      "description": "Chef John says this simple butter sauce is wonderful on fish, shrimp, and lobster."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2021%2F11%2F04%2Fimage-144.jpg",
      "title": "Lemon-Butter Shortbread Cookies",
      "url": "https://www.allrecipes.com/recipe/273880/lemon-butter-shortbread-cookies/",
      "description": "If the idea of buttery, tender lemon shortbread isn't enough to tempt your taste buds, these cookies are dipped in a lemon glaze, too. Recipe creator Cindy My Country Table says, \"Cookies taste more lemony the next day.\""
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F2002595.jpg",
      "title": "Garlic-Herb Butter Drop Biscuits",
      "url": "https://www.allrecipes.com/recipe/240682/garlic-herb-butter-drop-biscuits/",
      "description": "These drop biscuits are made with lots of real butter, Cheddar cheese, seasonings, and herbs — the resulting biscuit is fluffy and flavorful!"
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F2017749.jpg",
      "title": "Raisin Butter Tart Squares",
      "url": "https://www.allrecipes.com/recipe/239963/raisin-butter-tart-squares/",
      "description": "A brown sugar crust and filling give these gooey butter tarts their rich, warm flavor."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F8429504.jpg",
      "title": "Garlic-Butter Roasted Mushrooms",
      "url": "https://www.allrecipes.com/recipe/281241/garlic-butter-roasted-mushrooms/",
      "description": "Melted butter, garlic, Parmesan cheese, and fresh parsley transform run-of-the-mill white mushrooms into a flavorful side dish. \"My favorite way to serve these is with a juicy grilled ribeye,\" says recipe creator and Allrecipes Allstar France C."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F4458844.jpg",
      "title": "Buttered-Braised Cabbage",
      "url": "https://www.allrecipes.com/recipe/256279/buttered-braised-cabbage/",
      "description": "Cabbage gets sweeter as its cooked, but when braised in butter, even the most ardent cabbage hater can't resist."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F7617251.jpg",
      "title": "Air Fryer Lobster Tails with Lemon-Garlic Butter",
      "url": "https://www.allrecipes.com/recipe/276006/air-fryer-lobster-tails-with-lemon-garlic-butter/",
      "description": "Forget the grill or oven, the air fryer makes juicy, tender lobster in a matter of minutes. This recipe features a lemon-garlic butter for slathering on top. \"I will never cook lobster in anything other than an air fryer again!\" says Allrecipes Allstar Soup Loving Nicole."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2021%2F11%2F04%2Fimage-75.jpg",
      "title": "Chef John's Hot Buttered Rum",
      "url": "https://www.allrecipes.com/recipe/282572/chef-johns-hot-buttered-rum/",
      "description": "\"While eggnog gets a lot more press, hot buttered rum is the ultimate festive holiday drink,\" says Chef John. \"So rich, so delicious, so satisfying, and super easy to make.\""
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F5598867.jpg",
      "title": "Carolina Butter Pecan Cake Bars",
      "url": "https://www.allrecipes.com/recipe/260040/carolina-butter-pecan-cake-bars/",
      "description": "A buttery pecan cake is slathered in a cream cheese frosting and served chilled: \"Yum.. took these to church and everyone loved them,\" says Allrecipes Allstar Linda T."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F3447150.jpg",
      "title": "Cast Iron Buttermilk Biscuits",
      "url": "https://www.allrecipes.com/recipe/246399/cast-iron-buttermilk-biscuits/",
      "description": "These old-fashioned buttermilk biscuits are baked in a hot, buttered cast iron skillet for maximum flavor."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F4480942.jpg",
      "title": "Ultimate Butter Pound Cake",
      "url": "https://www.allrecipes.com/recipe/257279/ultimate-butter-pound-cake/",
      "description": "Serve this dense, buttery pound cake with seasonal berries and whipped topping!"
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F2061923.jpg",
      "title": "Gina's Italian Butter Cookies",
      "url": "https://www.allrecipes.com/recipe/279153/ginas-italian-butter-cookies/",
      "description": "Recipe creator NIGGI832 describes these cookies as, \"Traditional Italian-American bakery-style butter cookies that will make you feel like you bought them from your favorite local bakery in New York! Fill them with raspberry or apricot preserves, or chocolate, or dip one side in chocolate and cover with sprinkles — or do both!\""
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F2258386.jpg",
      "title": "Cheddar Biscuits with Chive Butter",
      "url": "https://www.allrecipes.com/recipe/241470/cheddar-biscuits-with-chive-butter/",
      "description": "When spring brings with it fresh chives, make these Cheddar biscuits served with a chive butter."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F1128226.jpg",
      "title": "Plantains in Butter Rum Sauce",
      "url": "https://www.allrecipes.com/recipe/237445/plantains-in-butter-rum-sauce/",
      "description": "These butter rum plantains are best served over vanilla ice cream."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F5929618.jpg",
      "title": "Gooey Sweet Potato Butter Cake",
      "url": "https://www.allrecipes.com/recipe/268678/gooey-sweet-potato-butter-cake/",
      "description": "This easy sweet potato butter cake is cooked in a 9x13-inch baking dish, making it great for the holidays or any time you're serving a crowd."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F9198136.jpg",
      "title": "Butterscotch Pull-Apart Rolls",
      "url": "https://www.allrecipes.com/recipe/263698/butterscotch-pull-apart-rolls/",
      "description": "These pull-apart rolls can be prepared the night before and popped in the oven when it's time to serve."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F4566744.jpg",
      "title": "High-Rise Buttermilk Biscuits",
      "url": "https://www.allrecipes.com/recipe/261050/high-rise-buttermilk-biscuits/",
      "description": "Follow this technique for making the fluffiest, airiest, high-rise biscuits. Serve with homemade raspberry jam."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F8746567.jpg",
      "title": "Fingerling Potatoes with Tarragon Chive Butter",
      "url": "https://www.allrecipes.com/recipe/270719/fingerling-potatoes-with-tarragon-chive-butter/",
      "description": "Steamed fingerling potatoes are tossed in in a mixture of butter, garlic, creme fraiche, and fresh herbs."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F4463868.jpg",
      "title": "Garlic Buttermilk Mashed Potatoes",
      "url": "https://www.allrecipes.com/recipe/246557/garlic-buttermilk-mashed-potatoes/",
      "description": "Buttermilk brings its signature tang to creamy mashed potatoes. Reviewer Margie Robinson says, \"Never made mashed potatoes using buttermilk before and this was excellent! I used the leftovers and made gnocchi with it...omg, amazing!\""
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F7261279.jpg",
      "title": "Freezer Butter Cookies",
      "url": "https://www.allrecipes.com/recipe/274469/freezer-butter-cookies/",
      "description": "\"Make a double or triple batch of these heavenly cookies. Roll the dough into logs, freeze, and delicious warm cookies are always only minutes away any time you or the kids want them,\" says recipe creator Kristine."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F7882482.jpg",
      "title": "Instant Pot Butter Chicken from Frozen",
      "url": "https://www.allrecipes.com/recipe/279530/instant-pot-butter-chicken-from-frozen/",
      "description": "Make your own version of this popular Indian dish in the Instant Pot— chicken is pressure cooked in a buttery, tomato-based sauce."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F7890453.jpg",
      "title": "Bread and Butter Pudding",
      "url": "https://www.allrecipes.com/recipe/279519/bread-and-butter-pudding/",
      "description": "\"This simple bread pudding is an easy way to use up those bits and pieces that seem to lie around the pantry,\" says the recipe creator Diana Moutsopoulos. Stale bread, butter, sugar, dried currants, milk, eggs, and nutmeg make up this pantry-staple dessert."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F4582585.jpg",
      "title": "Honey Butter Biscuits",
      "url": "https://www.allrecipes.com/recipe/258998/honey-butter-biscuits/",
      "description": "The honey butter filling keeps these biscuit rolls from drying out in addition to adding sweet flavor."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F4461503.jpg",
      "title": "Butter Crackers",
      "url": "https://www.allrecipes.com/recipe/255535/gluten-free-butter-crackers/",
      "description": "This recipe mimics the rich taste of butter crackers, but without the gluten."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6374365.jpg",
      "title": "Homemade Cookie Butter",
      "url": "https://www.allrecipes.com/recipe/270704/homemade-cookie-butter/",
      "description": "Flavored with speculoos cookies, this homemade cookie butter adds its sweet, brown sugar-cinnamon to everything it touches."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F7577581.jpg",
      "title": "Garlic Butter Smoked Shrimp",
      "url": "https://www.allrecipes.com/recipe/278091/garlic-butter-smoked-shrimp/",
      "description": "A lemon, garlic, and butter mixture adds flavor to smoked shrimp without taking away from the naturally smoky flavor."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6803230.jpg",
      "title": "Blueberry-Lemon Butter Cookies",
      "url": "https://www.allrecipes.com/recipe/274283/blueberry-lemon-butter-cookies/",
      "description": "Lemon and blueberries were made for each other, and they mingle beautifully in these classic butter cookies. The dough can be made ahead of time and frozen until you're ready to bake."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F9096163.jpg",
      "title": "Baked Lemon-Butter Salmon",
      "url": "https://www.allrecipes.com/recipe/283204/baked-lemon-butter-salmon/",
      "description": "This buttery salmon bakes up crispy on the outside and tender and juicy on the inside."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F7795273.jpg",
      "title": "Sous Vide Mahi Mahi with Jalapeno-Lime Butter",
      "url": "https://www.allrecipes.com/recipe/279168/sous-vide-mahi-mahi-with-jalapeno-lime-butter/",
      "description": "\"Traditional methods of cooking mahi mahi can leave it dry, but cooking it sous vide in its own juices ensures tender and moist results,\" says recipe creator France C.  The jalapeño-lime butter adds bright, zesty flavor to mild mahi mahi."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F1984031.jpg",
      "title": "Buttery Sugar Pretzels",
      "url": "https://www.allrecipes.com/recipe/240843/buttery-sugar-pretzels/",
      "description": "Melted butter and powdered sugar jazz up store-bought pretzels. For sugar cookie-flavored pretzels, try using sugar cookie mix in place of the sugar, as recipe creator Audrey suggests."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F5922538.jpg",
      "title": "Butterbeer Sugar Cookies",
      "url": "https://www.allrecipes.com/recipe/268681/butterbeer-sugar-cookies/",
      "description": "These Harry Potter-inspired cookies mimic the flavor of butterbeer using brown sugar, maple syrup, pumpkin pie spice, and, of course, lots of butter."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F9427617.jpg",
      "title": "Gingerbread Gooey Butter Cookies",
      "url": "https://www.allrecipes.com/recipe/286022/gingerbread-gooey-butter-cookies/",
      "description": "Allspice, nutmeg, cloves, brown sugar, molasses, and almond extract add warm, nutty flavor to these ooey-gooey crinkle cookies."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F7474053.jpg",
      "title": "Danish Butter Cookies",
      "url": "https://www.allrecipes.com/recipe/277786/danish-butter-cookies/",
      "description": "Danish butter has a higher fat content than American-style butter, which makes all the difference in these iconic holiday cookies. Be sure to make a double batch for gifting!"
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fimages.media-allrecipes.com%2Fuserphotos%2F6979849.jpg",
      "title": "Brown Butter Blondies",
      "url": "https://www.allrecipes.com/recipe/275713/brown-butter-blondies/",
      "description": "Browning butter is a French technique that adds warm, nutty flavor to both sweet and savory dishes. Here it's combined with chocolate chips and chopped nuts in blondies."
    },
    {
      "image": "https://imagesvc.meredithcorp.io/v3/mm/image?url=https%3A%2F%2Fstatic.onecms.io%2Fwp-content%2Fuploads%2Fsites%2F43%2F2022%2F01%2F27%2FScreen-Shot-2022-01-26-at-10.15.40-PM.png",
      "title": "More Butter Recipes",
      "description": ""
    },
    {
      "title": "",
      "description": ""
    }
  ]
}
```

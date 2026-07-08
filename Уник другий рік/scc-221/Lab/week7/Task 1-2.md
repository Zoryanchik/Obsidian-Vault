Task 1: Recipe
![[Pasted image 20260105192557.png]]
{
	"name": "Perfect chocolate brownies",
	"URL": "https://www.bbc.co.uk/food/recipes/richchocolatebrownie_1933",
	"description": "This is our most perfect chocolate brownie recipe. It's everything you want in a brownie – fudgy, dark and chocolatey. Serve these brownies warm with a scoop of vanilla ice cream and you'll understand what happiness is.",
	"servings": 20,
	"ingredients": [
		{
			"item": "butter",
			"weight": "225g",
			"note": "preferably unsalted"
		},
		{
			"item": "caster sugar",
			"weight": "450g"
		},
		{
			"item": "dark chocolate",
			"weight": "140g",
			"note": "broken into pieces"
		},
		{
			"item": "eggs",
			"quantity": 5,
			"note": "free-range medium"
		},
		{
			"item": "plain flour",
			"weight": "110g"
		},
		{
			"item": "cocoa powder",
			"weight": "55g"
		}
	],
	"steps": [
		"Heat the oven to 190C/170C Fan/Gas 5. Line a 20x30cm/8x12in baking tin with baking paper.",
		"Gently melt the butter and the sugar together in a large pan. Once melted, take off the heat and add the chocolate. Stir until melted.",
		"Beat in the eggs, then stir in the flour and the cocoa powder.",
		"Pour the brownie batter into the prepared tin and bake for 30–35 minutes, or until the top of the brownie is just firm but there is still a gentle wobble in the middle.",
		"Take out of the oven and leave to cool in the tin. Cut the brownies into 5cm/2in squares when only just warm, or completely cool."
	]
}


Task 2
![[Pasted image 20260105192649.png]]
2.1

{
	"customer": "Jess Ventura",
	"address": "250 S Grand Ave, Los Angeles, California, USA",
	"items": [
		{
			"product": "Baking tin",
			"size": "20x30cm",
			"brand": "Circulon",
			"quantity": 1,
			"price": 21.99
		},
		{
			"product": "Cooking chocolate",
			"size": "100g",
			"brand": "Menier",
			"quantity": 2,
			"price": 1.99
		},
		{
			"product": "Cocoa powder",
			"size": "150g",
			"quantity": 1,
			"price": 2.99
		}
	],
	"total": 28.96,
	"order date": "2025-10-10",
	"status": "shipped"
}


2.2:
**How it works:** The customer details and the full product details are stored _inside_ the order itself.
{
	"_id": "<ObjectID1>",
	"customer": {
		"name": "Jess Ventura",
		"address": "250 S Grand Ave, Los Angeles, California, USA"	
	},
	"items": [
		{
			"product": "Baking tin",
			"size": "20x30cm",
			"brand": "Circulon",
			"quantity": 1,
			"price": 21.99
		},
		{
			"product": "Cooking chocolate",
			"size": "100g",
			"brand": "Menier",
			"quantity": 2,
			"price": 1.99
		},
		{
			"product": "Cocoa powder",
			"size": "150g",
			"quantity": 1,
			"price": 2.99
		}
	],
	"total": 28.96,
	"order date": "2025-10-10",
	"status": "shipped"
}


2.3:
(this is in an array for a valid JSON of multiple objects)
In this version, the data is split into separate pieces that link to each other using IDs (like `ObjectID`).
[
    {
        "_id": "<ObjectID1>",
        "customer": "<ObjectID2>",
        "items": [
            {
                "item": "<ObjectID3>",
                "quantity": 1
            },
            {
                "item": "<ObjectID4>",
                "quantity": 2
            },
            {
                "item": "<ObjectID5>",
                "quantity": 1
            }
        ],
        "total": 28.96,
        "order date": "2025-10-10",
        "status": "shipped"
    },
    {
        "_id": "<ObjectID2>",
        "name": "Jess Ventura",
        "address": "250 S Grand Ave, Los Angeles, California, USA"
    },
    {
        "_id": "<ObjectID3>",
        "product": "Baking tin",
        "size": "20x30cm",
        "brand": "Circulon",
        "price": 21.99
    },
    {
        "_id": "<ObjectID4>",
        "product": "Cooking chocolate",
        "size": "100g",
        "brand": "Menier",
        "price": 1.99
    },
    {
        "_id": "<ObjectID5>",
        "product": "Cocoa powder",
        "size": "150g",
        "price": 2.99
    }
]
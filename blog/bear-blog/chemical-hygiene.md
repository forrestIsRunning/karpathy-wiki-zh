---
title: "Chemical hygiene"
date: 2025-12-18
url: https://karpathy.bearblog.dev/chemical-hygiene/
---

**中文翻译**

Karpathy 分享了他个人关于"化学卫生"的指南，涵盖水、空气、食物、布料、清洁用品等各个方面。

**水**：所有饮用水应来自反渗透（RO）过滤系统，最好安装台下式系统。还要安装全屋净水器。避免瓶装水和自来水。

**空气**：安装 HVAC 过滤器或空气净化器。避免在家中燃烧任何东西（蜡烛、燃气灶等）。避免加湿器和空气清新剂。

**食物**：最难控制的类别。买有机水果蔬菜，野生捕捞的太平洋三文鱼，牧场散养的鸡蛋/奶制品，有机空气冷却的鸡肉。加工食品要看配料表——越短越好。烹饪只用不锈钢或铸铁锅，不用不粘锅。储存用玻璃或不锈钢容器。不用塑料。

**布料**：只用天然纤维（棉、麻、羊毛、丝绸）。避免聚酯、尼龙等人造纤维。

**清洁用品**：选择成分简单、"无香精、无染料"的产品。

**牙齿卫生**：目前没有找到完美的无塑料替代品。

**防晒**：推荐矿物防晒霜（含氧化锌）而非化学防晒霜。

**健康**：有氧运动（多待在 Zone 2）、桑拿、补充维生素 D。

**核心思路**：保持家居简单。过滤水和空气。吃真正的食物。远离塑料。政府监管滞后，保护自己是你的责任。

---



Chemical hygiene

*18 Dec, 2025*

Following up on[digital hygiene](https://karpathy.bearblog.dev/digital-hygiene/), I wanted to write up my (evolving, opinionated) guide to chemical hygiene. I keep ranting about this topic to all of my friends recently (you can tell I'm really fun at parties), so I thought it would be worth writing it up to have it all in one place/url:

**Water**

Starting out with controlling your water system, which is the easiest in terms of concrete, high confidence recommendations that in my experience still only<5% of my friends have adopted:

- All your drinking water should come from**Reverse Osmosis**- the gold-standard Point of Use water filtration system, with a remineralization post filter. Ideally install an under the sink system, but fallback to countertop systems is ok. Brita and other basic filters are not good enough to adequately filter your drinking water.
- In addition, install a whole-home water filter (usually sediment+carbon, not Reverse Osmosis, that would be impractical), to enjoy cleaner water in your entire home, including shower, dishwasher, laundry, etc. If that's too expensive or impossible (e.g. you're renting), at least install a shower filter.
- Avoid drinking water from water bottles, certainly from plastic bottles but also in general. You cannot control that supply chain, both during collection but also during delivery (especially light, heat).
- Avoid drinking tap water, it's a lot less clean than you'd think (it is relatively poorly treated centrally*and*then it has to be delivered to your home through undefined pipes) and, with proper dental care, includes unnecessary and possibly mildly harmful "public health" additives especially and controversially fluoride.[Example fun study](https://jamanetwork.com/journals/jamanetworkopen/fullarticle/2833716): people living near golf courses (which are heavily treated with pesticides) show an increased risk for Parkinson Disease.

Water is the easiest section in this entire article because it has well-understood ways to spend $/risk reduction compared to a lot more complex categories we'll see later (food especially). I would recommend contacting a company in your local area to install both a whole home filter and an under-the-sink reverse osmosis system, to handle the ~yearly maintenance (filter changes), and conduct tests to demonstrate the improvement.

**Air**

Similar to water, air is relatively well-understood and simple to control in your home:

- Install HVAC filters, and/or get a standalone air purifier, e.g. I got the[Dyson Big+Quiet](https://www.dyson.com/air-treatment/air-purifiers/big-quiet-formaldehyde)because it's quite good, HEPA grade and doubles as a cool looking alien artifact in your room, but for the top top performance I'd get[IQAir GC MultiGas XE](https://www.amazon.com/IQAir-MultiGas-Air-Purifier-Filtration/dp/B0D7M5XX6C)- this is the tier of product a hospital reaches for during an airborne virus outbreak.
- Avoid combustion in your home in general - it's a source of all kinds of fumes and partial combustion products:
- Avoid candles (use beeswax only if you really like them, I do occasionally)
- Avoid gas stoves (use induction cooktop)
- Avoid unsealed gas fireplaces. Use sealed, electric ignition only.
Skip air humidifiers unless you really live in very dry conditions, otherwise they come with mold/bacterial risks unless they are very properly taken care ofSkip all air fresheners, oil diffusers and all kinds of fragrances, they are a very poorly regulated wild west of synthetic chemicals.Measure the basics of your home air quality. Example device[I bought](https://www.amazon.com/dp/B0FXDQX5XQ)recently.Like water, testing air is easy - call a professional to do a more comprehensive test panel for the air in your home, e.g. including Radon which can come up from the ground, mold, spores, etc.

**Food**

Food is the hardest category to control because it involves extensively deep supply chains that have been ruthlessly efficiency-maxxed over the last few decades with little to no regard for public health externalities. The industry has a clear and immediate financial incentive to trade something 10% cheaper at the cost of something 10X more harmful to you as long as it shows up over a long enough time period that the accounting is impractical. And it just turns out that in food there are many, many ways to cut corners. Sadly, the US Government has been woefully inadequate in constraining the industry and lags far behind other countries (e.g. Europe especially), hence the recent[MAHA](https://en.wikipedia.org/wiki/Make_America_Healthy_Again)efforts. I'll split this section into 1) food sourcing and 2) cooking/preparation.

**Food: 1) sourcing**

- Fruits/veggies: buy[organic](https://www.ams.usda.gov/sites/default/files/media/Organic%20Practices%20Factsheet.pdf), which restricts a large variety of chemical treatments. - the label (PLU) will usually start with 9*.
- Salmon: look for "Pacific" (not Atlantic) and "wild-caught" (not farmed). Farmed salmon come from overcrowded farms in un-natural conditions that mix chemicals, disease and parasites, and diet supplements to make them have the right color.
- Eggs/dairy: Look for "Pasture raised" (all the other adjectives like "cage free" and "free range" are scams and not what it sounds like[video 1](https://www.youtube.com/watch?v=qpeu0guMKw4),[video 2](https://www.youtube.com/watch?v=fpO3Y5yVVIA)as example pointers), and "organic".
- Chicken: Look for 1) "pasture raised", 2) "organic" and 3) "Air-chilled" if you don't like the idea of your chicken taking a[chlorine bath](https://www.youtube.com/watch?v=qzonOHC49Us). Yes you read that right, it's a standard practice in the US that has been banned in Europe since 1997.
- Packaged goods: Look at the ingredients list. It should be short. It should make sense. For example, your bread should not be 50 ingredients that you can't pronounce, it should be 4 (flour, water, salt, and yeast). Use apps like[BobbyApproved](https://apps.apple.com/us/app/bobby-approved-food-scanner/id1571725006)and[Ivy](https://apps.apple.com/us/app/ivy-processed-food-scanner/id6642701963)to scan the bar codes and get a lot of information about all ingredients and a score (I like and use both).
- Don't buy "edible food-like substances", which are usually lining the shelves on the inner shelves of your supermarket. Shop only at the walls, which contain real food - fruits/veggies, dairy, meat, breads. For example, fruit loops and such are NOT food and routinely contain harmful ingredients that I'm frankly shocked are legal, many of which are banned in Europe and elsewhere in the world.
- Avoid canned soups/products.
- Avoid touching receipts, they are laced with BPA/BPSs (endocrine disruptors).
- Consider getting a home delivery service, e.g. I currently like and use[Locale](https://www.shoplocale.com/).

![GvWK5b1X0AEevjd](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/gvwk5b1x0aeevjd.webp)

Example food, and what a grocery store should look like. From this[tweet](https://x.com/karpathy/status/1942612984481870068), with a bit more discussion.

**Food: 2) Cooking & preparation**

- Rule number 1: avoid plastics, specially in combination with heat.
- Use only stainless steel or cast iron pans only. Don't use non-stick (teflon etc)
- Storage: use non-plastic containers like glass, stainless steel, ceramic
- Cutting boards: wooden only
- Utensils: wooden, metal cookware
- Blenders: glass or stainless steel, don't allow your food to mix at high velocities with plastics, they will chip into your food.
- Don't Doordash hot food that comes in plastic containers
- Don't microwave food in plastic containers to prevent leeching. Transfer food to microwave-safe non-plastic plates.
- Don't use the yellow sponges (use cotton, loofa, stainless steel scouring pad)
- No hot coffee or liquids in disposable cups (e.g. Starbucks), they are all lined with plastic. Bring a mug with you ideally, or ask "for here" if you can.
- No hot coffee from cheap coffee machines (e.g. Keurig, again - they pass hot liquids through plastic components).
- Do not use tea bags, they contain plastics and chemicals that leech into your tea. Only buy and use loose leaf tea with a stainless steel strainer.
Cooking oil: Seed oils are currently hotly contested. Personally I find them highly suspicious and prefer to use clean oils: extra virgin olive oil (ideally at lower temperatures), avocado oil (cooking), or butter, ghee, beef tallow (frying).Your kitchen should basically be all wood, stainless steel, glass, ceramic, and for any fabrics only the natural kind (cotton, bamboo, linen, wool, etc.).

**Fabrics**

Our bodies come into frequent contact with all kinds of fabrics (clothing, bedding, furniture, rugs, mats, ...). As you handle these materials, they shed particles, which you end up breathing in.

- Again, avoid the pervasive toxic petroleum-based plastics industry - these fibers are much cheaper (which is why they found their way everywhere), but they shed nano/micro plastics that are steeped in a zoo of chemical additives (plasticizers).
- Only use natural fibers: cotton, linen, hemp, wool, silk, bonus points for organic, bonus points for extra certifications (e.g. GOTS). You'll see that the use of plastics in fabrics (e.g. clothes) is*pervasive*. They've really snuck them everywhere. If you didn't pay too much attention so far, your clothes almost certainly have polyester, nylon, spandex, etc. Your rug is almost certainly polyester.
- Be wary of "bamboo" which sounds natural but there is a pervasive and sketchy trick that the industry already got sued over by the FTC in 2010 for deceptive marketing. It's not bamboo, it's cellulose that gets heavily chemically processed into fibers called rayon/viscose.

**Cleaning supplies: soap, dish washing, laundry, toilet, spray cleaners**

- Look for very few and simple ingredients and ideally "fragrance free" and "dye free". I currently use[Blueland](https://www.blueland.com/)for all of these.

**Dental hygiene**

This is a category that I was not able to make a dent into in my personal life, despite a number of attempts. The goal with all of this is go after the 80:20 low hanging fruit and this category for me falls into the latter category:

- Toothbrush - it won't surprise you that heavy rubbing of plastic bristles over your teeth sheds some of the material. Again don't fall for "bamboo" scams when browsing toothbrushes on Amazon. These products aren't what people imagine, they are synthetics, the bristles still have polyester or nylon and etc. I did eventually find actually plastic-free toothbrushes (see e.g.[Primal](https://primals.shop/products/primals-horse-bristle-bamboo-toothbrush-4-pack)) that have bristles from horse/boar hair, but to be honest they are not as comfortable so I still use plastic bristle toothbrush today.
- Floss - same story as toothbrush. The only actually natural type you can get is silk floss, but it's a bit more brittle than what you're probably used to and I couldn't find one in the much easier to use pick form. I still use plastic floss right now and I am experimenting with water floss.
- Toothpaste - it seems very trendy to diss on fluoride but I'm not personally convinced just yet and I still use a fluoride toothpaste.

**Sunscreen**

- Most sunscreens are*chemical*. I prefer mineral sunscreens, which simply create a layer on top of the skin that acts as a physical barrier to UV (e.g. look for Zinc), though unfortunately they do create a "chalky" look. Chemical sunscreens seep into the skin (and blood) and there are concerns over some of their ingredients and their potential to act as endocrine disruptors. I should add that I'm a little bit suspicious of the need and overuse of sunscreen in general and I personally apply it only in cases of prolonged, intense exposure of my computer scientist vampire skin to high UV index sun. Check your Weather app to see the UV Index for the time of day of your exposure.
- I am much less well-versed in cosmetics more generally because I don't personally use these products but I wouldn't at all be surprised if it is a major minefield.

**Wellness**

- Cardio (make sure to do it properly - most people spend way too much time in Zone 3+, spend a lot more time in Zone 2)
- Sauna ([shown](https://blueprint.bryanjohnson.com/blogs/news/is-sauna-worth-the-hype)to reduce the inevitably accumulated toxins via sweat)
- Vitamin D - you're probably deficient like everyone else. Blood is relatively easy to test and I encourage people to do a full panel ~yearly to track health and deficiencies.

**Learn more**

- Recommended watching: I now use my Instagram for more non-AI / lifestyle related things, e.g. see the reposts section on[my account](https://www.instagram.com/karpathy/)for some of the featured reels that I've accumulated over time on the topics above.
- Recommended reading:["Poison like no other"](https://www.amazon.com/Poison-Like-Other-Microplastics-Corrupted/dp/1642832359)(on plastics),["In Defense of Food"](https://www.amazon.com/Defense-Food-Michael-Pollan/dp/1594133328)(on food vs. "edible food-like substances"),["Poison Squad"](https://www.amazon.com/Poison-Squad-Chemists-Single-Minded-Twentieth/dp/1594205140),["Metabolical"](https://www.amazon.com/Metabolical-Processed-Nutrition-Modern-Medicine/dp/0063027712).
- Even doing all of the above you are simply decreasing risk, you can never eliminate it. For example, when[plasticlist.org](https://www.plasticlist.org/)tested various foods/drinks for plastics, they found a lot of random items that have significantly higher plasticizer measurements than others, in a way you'd never be able to guess. For example, at the time the worst offender by far was Boba guys - your boba would give you a significantly higher dose than any runner up, having to do with some process somewhere in their deep supply chain. Another example I encountered was a farm where to cut costs they didn't bother to remove the plastic wrap from their hay and allowed the cows to just eat all of it together, leading to milk from that specific farm that then tested significantly higher in plasticizers. Unfortunately there is not enough testing, scrutiny and oversight over these deep supply chains by the government.
- There's so much more I didn't even cover in this guide. E.g. why modern wheat is so hyper-optimized to grow fast (which you can measure and profit from) at the cost of lacking nutrients (which the consumer won't normally measure) compared to ancient grains like einkorn. Or why[modern honey](https://www.youtube.com/watch?v=mCALGI1r4WY)is basically just glucose syrup compared to actual miracle food that medieval honey was. The cost-driven hyper-optimization of the industry is a deep rabbit hole way beyond the scope of this post. There are too many ways to cut corners and make something cheaper by sacrificing its nutrients and/or by risking longer term public health. If I can convince a few people to at least start paying attention, its goal will have been met.

**TLDR**. Keep your home unsophisticated. Filter your water and air. Eat real food (not edible food-like substances) from well-treated animals and with few, sensible ingredients and minimally sophisticated supply chains and processing steps. Say no to as many dyes and fragrances as you can. Surround yourself with simple, natural materials or strong and inert materials (e.g. stainless steel). Avoid plastics, especially if they are handled, heated, frozen - the risk is not just related to the tiny particles of these exotic materials accumulating[all over your body](https://hscnews.unm.edu/news/hsc-newsroom-post-microplastics-human-brains)and interfering with its chemistry, but the large zoo of chemical[plasticizers](https://en.wikipedia.org/wiki/Plasticizer)that are added to plastics and then leech out. The government is significantly lagging behind the industry on chemical regulation and this is*your*responsibility.

This guide isn't perfect. It's a work in progress. I am not a professional toxicologist or food scientist so my tone above is my frustration that the government is forcing me to be a part-time investigative journalist just to exist in a modern society and not feel like I am poisoning myself and my family. And I didn't even go into and cover all of the environmental aspects of these industries. This state of affairs is much worse here in the US than e.g. in Europe - the EU bans or restricts many food additives, dyes, chemicals and food processing practices that are routine here. The FDA "Generally Recognized As Safe" (GRAS) system lets manufacturers self-certify ingredients without independent review and a new exotic chemical or process is innocent until proven guilty, while in Europe the default is often the reverse. So treat all of this as a starting point, ask your favorite LLM for more information on any of the items, let me know your thoughts (e.g. X/Instagram DMs) and I will aim to update this guide over time.
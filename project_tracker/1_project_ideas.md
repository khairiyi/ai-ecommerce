# Section 1: project overview
-----------------------------------------------------------
Project background: I want to create an ai tool that empower chinese brand owners and manufacturers to better advertise, market their products; to better refine their existing produtcts for their targeted audiences; to get a professional designed branding building strategy. 

Targeted users: small to medium manufacturers and brand owners in China, whose main market of sale is the United States

My solution:
1. Leverage from founders's Chinese and US background, and use AI to build automated workflows that provide end to end solutions and help these customers to advertise, refine their existing products. Or create market-proven ideas to create new products. 

My Advantanges: 
1. These users cannot afforard an US-based agency to fully localize their products
2. The local teams have little knowledge on successfully advertise to the tartgeted audience
3. even with the help of ai tools, they do have a good grasp of the entire US technical eco-system, or advertising expertise. 

Major component of this AI tool should contain:

## Industry Knowledge Agent: 
This agent should automatically fetch and research the best practices, industry-specific knowledges. It will then create and main a library of these knowledge across industries. It will create a daily news letter that gives out a summary of below:
- major platforms' rules udpates
- macro regulations udpates
- latest market trends
    - reddit, tiktok, google to find the trending keywords
- competitors updates: pricing, product changes

## Branding & Strategy Agent
This agent create a branding and strategy plan for the brand/product. 

## Image to Video Agent:
This agent is capable to create commercial-level, or authentic UGC videos with different AI models. It would take in inputs of 
a. industry-specific from industry knowledge agent, and then modify the video generation prompt template. 
b. additioanl input of specific video requirements for each video generation 
c. actively or passively building video prompt templates for different purposes: e.g., showcasing a product, influencer advertising in selfie style, professioal commercials. 
c. obtain the latest knowledge on prompt engineering, and modify the video prompt to create videos in each video LLM. 

## media management agent
a. create and manage the scheduling of the creatives generation in the previous 'image to video agent'
b. upload these creatives to social platforms with the pre-determined schedules
4. customer engagement agent
a. this agent would responde to comments and messages on social medias and consolidate inquiries that are sales lead back to the brand owner

## Analytics Agent
This agent would analyze the data and extract insights to give new product recommendations, product feedback back to the brand ownswer. It will also generate and upate live dashboard for the stakeholders to monitor the insights
- ad spending across different platforms
- top performing videos
- alert: 
    a. GMV dropping over xx% 
    b. conversion rate change in xx channels
    c. SKU inventories dropping low
    d. video/photo CTR dropped

## Store/listing Management Agent
This agent would automatically manage and upload product listings to major ecommerce platforms like Amazon, Shopify and etc., 



# Section 2: Win over new business customers
-----------------------------------------------------------

Business Customer User Journey & Agent Use Case:
1. Collect new product's unique information:
    a. customer's goal, requirements
    b. unique information source: websites, social media accounts, competitor names

Industry Agent: 
a. Store customer's unique requirements in the database
b. Quickly do web search, parse through website information and create the initial industry knowledge base for this product

2. Ask for long-term goals or short-term goals:
    a. long-term brand positioning and goals(optional)
    b. short-term goals: get impressions, get conversions and etc.,

Branding & Strategy Agent:
a. input all brand's information to the agent
b. search for industry knowledge and competitors information
c. come up with a social media plan

3. Ask for product photos and create a first set of videos

Image to Video Agent: collect information from Industry Agent daily, and promptly update each day's video creation if necessary(ex: breaking news)

4. Automatically uploading the videos to desired social media platforms on a schedule created in step 2.

Media Management Agent:

5. Show centralized data

Analytics Agent


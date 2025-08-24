<p align="center">
    <img src="https://github.com/user-attachments/assets/219f2dbc-37ed-4aea-a289-ba39cdbb335d" alt="Pydoll Logo" /> <br>
</p>
<h1 align="center">Pydoll: Automate the Web, Naturally</h1>

<p align="center">
    <a href="https://codecov.io/gh/autoscrape-labs/pydoll" >
        <img src="https://codecov.io/gh/autoscrape-labs/pydoll/graph/badge.svg?token=40I938OGM9"/>
    </a>
    <img src="https://github.com/autoscrape-labs/pydoll/actions/workflows/tests.yml/badge.svg" alt="Tests">
    <img src="https://github.com/autoscrape-labs/pydoll/actions/workflows/ruff-ci.yml/badge.svg" alt="Ruff CI">
    <img src="https://github.com/autoscrape-labs/pydoll/actions/workflows/mypy.yml/badge.svg" alt="MyPy CI">
    <img src="https://img.shields.io/badge/python-%3E%3D3.10-blue" alt="Python >= 3.10">
    <a href="https://deepwiki.com/autoscrape-labs/pydoll"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a>
</p>

<p align="center">
  📖 <a href="https://pydoll.tech/">Documentation</a> •
  🚀 <a href="#-zero-to-hero-in-seconds">Zero to Hero</a> •
  ⚡ <a href="#-standout-features">Standout Features</a> •
  🛠️ <a href="#-advanced-magic">Advanced Magic</a> •
  💖 <a href="#-support-the-project">Support</a>
</p>
<br>

You know that feeling when you need to automate something on the web and you spend hours just trying to get your environment working? We've all been there.

**Pydoll changes that.**

Built from scratch with one simple philosophy: **it should just work.** No drivers to install, no PATH variables to configure, no dependency hell, no compatibility nightmares.

Just `pip install pydoll-python` and you're automating.

<div align="center">
  <h4>Give it a star if you appreciate tools that just work! ⭐</h4>
  <sub>(Your stars fuel our development and bug fixes)</sub>
</div>
<br>


#### **Zero configuration. Zero drivers. Zero headaches.**
```python
# This is literally all you need:
from pydoll.browser import Chrome

async with Chrome() as browser:
    tab = await browser.start()
    await tab.go_to('https://example.com')
    # You're automating. That's it.
```

#### **Async-first architecture for performance**
Built from day one for async/await. Run multiple tabs simultaneously with true concurrency:
```python
# Multiple tabs? Multiple sites? No problem.
tasks = [
    scrape_site1(tab1),
    scrape_site2(tab2), 
    scrape_site3(tab3)
]
results = await asyncio.gather(*tasks)  # Fast concurrent execution
```

#### **Intuitive API design**
Finding elements feels like natural language:
```python
# This reads like English:
button = await tab.find(tag_name='button', text='Click me', class_name='btn-primary')
await button.click()

# Or go fancy with XPath/CSS:
element = await tab.query('//div[@data-testid="awesome-element"]')
```

#### **Full type safety**
Every method, every parameter, every return value is fully typed. Your IDE becomes your best friend:
```python
# The IDE knows exactly what each call returns:
await tab.find(id='username')  # → WebElement
await tab.find(id='username', find_all=True)  # → list[WebElement] 
await tab.find(id='username', raise_exc=False)  # → WebElement | None

# Perfect autocomplete and error detection
await element.type_text('hello')  # IDE knows all available methods
```

#### **Human-like interactions**
Pydoll doesn't just click - it behaves like a real human. Natural mouse movements, realistic typing patterns, smart waits.

**Ethical Note**: Due to these realistic interaction patterns, Pydoll may bypass some behavioral detection systems. Please use responsibly and respect website terms of service.


#### **Just getting started?**

Impressed by what you've seen? **This is just the beginning!** 

Pydoll comes packed with advanced features that make complex automation scenarios effortless:

- **Event-driven automation** - React to page changes, network events, and user interactions in real-time
- **Request interception & monitoring** - Capture, modify, or block HTTP requests on the fly  
- **Complete keyboard simulation** - Full support for complex key combinations and realistic typing patterns
- **Network condition simulation** - Test how your automation behaves under different network speeds
- **Performance monitoring** - Built-in metrics for response times, resource loading, and more
- **Advanced stealth features** - Fine-tune browser fingerprints and behavioral patterns

**And this is just the beginning.** Check out our [complete documentation](https://pydoll.tech/) to discover everything Pydoll can do!



## 📦 **Installation**

```bash
pip install pydoll-python
```

**That's literally it.** No drivers, no additional downloads, no configuration files. Install and start automating in the next 30 seconds.



## 🚀 **Zero to Hero in Seconds**

### **Your first automation**
Let's do something cool - automated Google search that actually works:

```python
import asyncio
from pydoll.browser import Chrome
from pydoll.constants import Key

async def google_magic():
    async with Chrome() as browser:
        tab = await browser.start()
        
        # Navigate to Google
        await tab.go_to('https://google.com')
        
        # Find search box and search
        search_box = await tab.find(name='q')
        await search_box.type_text('Pydoll Python automation')
        await search_box.press_keyboard_key(Key.ENTER)
        
        # Click first result
        first_result = await tab.find(tag_name='h3', timeout=10)
        await first_result.click()
        
        print("🎉 Just automated Google like a boss!")

# Run it!
asyncio.run(google_magic())
```

**Run this code.** Watch your browser come alive. Feel the magic.

### **Data extraction made ridiculously easy**
```python
async def extract_github_data():
    async with Chrome() as browser:
        tab = await browser.start()
        await tab.go_to('https://github.com/autoscrape-labs/pydoll')
        
        # Extract data with readable code
        stars = await (await tab.find(id='repo-stars-counter-star')).text
        description = await (await tab.query(
            '//h2[contains(text(), "About")]/following-sibling::p')
        ).text
        
        print(f"⭐ Stars: {stars}")
        print(f"📝 Description: {description}")
        
        return {'stars': stars, 'description': description}
```

**Beautiful, readable, and it just works.**


## ⚡ **Standout Features**

### **Browser-Context HTTP Requests** 
*A powerful approach to hybrid automation*

Make HTTP requests that **automatically inherit** your browser's cookies, auth, and session state:

```python
# Login through the UI (human-like)
await tab.go_to('https://app.example.com/login')
await (await tab.find(id='email')).type_text('user@example.com')
await (await tab.find(id='password')).type_text('super-secret')
await (await tab.find(type='submit')).click()

# Now make API calls that inherit the session!
response = await tab.request.get('https://app.example.com/api/user/profile')
user_data = response.json()  # Automatically authenticated!

# POST data while staying logged in
await tab.request.post(
    'https://app.example.com/api/settings',
    json={'theme': 'dark', 'notifications': False}
)
```

**Why this matters:**
- **No session juggling** - cookies inherited automatically
- **No CORS headaches** - requests run in browser context  
- **No auth complexity** - login once, API forever
- **Hybrid workflows** - UI for auth, API for speed

### **Deep browser customization**
*Fine-tune every aspect of Chrome's behavior*

Want to completely customize Chrome's behavior? You have access to hundreds of internal settings:

```python
from pydoll.browser.options import ChromiumOptions

options = ChromiumOptions()

# Create your perfect automation environment
options.browser_preferences = {
    'download': {
        'default_directory': '/tmp/downloads',
        'prompt_for_download': False,  # Silent downloads
    },
    'profile': {
        'default_content_setting_values': {
            'notifications': 2,        # Block notifications
            'geolocation': 2,         # Block location requests
            'popups': 1,              # Allow popups for automation
        },
        'password_manager_enabled': False,
    },
    'browser': {
        'check_default_browser': False,
        'show_update_promotion_infobar': False
    }
}

async with Chrome(options=options) as browser:
    # Your browser is now perfectly configured for automation!
```

**Real-world applications:**
- **Silent everything** - downloads, notifications, prompts
- **Multi-region testing** - languages, timezones, locales  
- **Security lockdown** - disable cameras, mics, dangerous features
- **Stealth mode** - customize fingerprints and behavioral patterns

### **Bulletproof file downloads**
*No more download race conditions*

```python
# Downloads that actually work!
async with tab.expect_download(timeout=30) as download:
    await (await tab.find(text='Download Report')).click()
    
    # Wait for completion and get the file
    file_data = await download.read_bytes()
    print(f"📁 Downloaded {len(file_data)} bytes to {download.file_path}")
```

Auto-cleanup, timeout handling, and zero headaches included!


## 🛠️ **Advanced Magic**

### **Smart element finding**
*Find elements the way your brain thinks*

```python
# Natural language finding
submit_btn = await tab.find(
    tag_name='button',
    text='Submit',
    class_name='btn-primary',
    timeout=10
)

# Multiple ways to find the same thing
login_button = await tab.find(id='login')                    # By ID
login_button = await tab.query('button#login')              # CSS selector  
login_button = await tab.query('//button[@id="login"]')     # XPath
login_button = await tab.find(data_testid='login-btn')      # Custom attributes

# Find multiple elements
all_links = await tab.find(tag_name='a', find_all=True)

# Smart waiting and error handling
element = await tab.find(
    class_name='dynamic-content',
    timeout=15,
    raise_exc=False  # Returns None instead of throwing
)
```

### **Element state management**
*Wait for elements like a pro*

```python
element = await tab.find(id='submit-btn')

# Wait for the perfect moment to interact
await element.wait_until(is_visible=True, timeout=10)
await element.wait_until(is_interactable=True, timeout=5)

# Check states before acting
if await element.is_visible() and await element.is_on_top():
    await element.click()
    
# Execute custom JavaScript on elements
await element.execute_script("this.style.outline='2px solid red'")
```

### **Concurrent automation**
*Handle multiple tabs efficiently*

```python
async def scrape_multiple_sites():
    browser = Chrome()
    
    # Spin up multiple tabs
    tab1 = await browser.start()
    tab2 = await browser.new_tab()
    tab3 = await browser.new_tab()
    
    # Run them all concurrently
    results = await asyncio.gather(
        scrape_site('https://site1.com', tab1),
        scrape_site('https://site2.com', tab2),
        scrape_site('https://site3.com', tab3)
    )
    
    await browser.stop()
    return results

# Efficient concurrent execution
```

### **Custom browser configurations**
*Make Chrome behave exactly how you want*

```python
options = ChromiumOptions()

# Custom browser binary
options.binary_location = '/path/to/custom/chrome'

# Proxy configuration  
options.add_argument('--proxy-server=http://proxy:8080')

# Window and performance settings
    options.add_argument('--window-size=1920,1080')
options.add_argument('--disable-gpu')
options.start_timeout = 30  # For slower environments

# Docker-friendly settings
options.add_argument('--no-sandbox')
options.add_argument('--disable-dev-shm-usage')

    async with Chrome(options=options) as browser:
    # Fully customized browser experience
```



## 🎉 **What's New - Latest Release**

### **Smart WebElement state management**

We've made element interactions bulletproof with new state management:

```python
element = await tab.find(id='dynamic-button')

# Wait for perfect interaction conditions
await element.wait_until(is_visible=True, timeout=10)
await element.wait_until(is_interactable=True, timeout=5)

# New public methods for state checking
visible = await element.is_visible()        # Is it actually visible?
interactive = await element.is_interactable()  # Ready for clicks?
on_top = await element.is_on_top()         # Not covered by other elements?

# Execute JavaScript directly on elements
await element.execute_script("this.scrollIntoView()")
result = await element.execute_script("return this.innerText", return_by_value=True)
```

**No more flaky tests or missed clicks!** These methods ensure your automation is rock-solid reliable.


## **Troubleshooting**

**Browser not found?**
```python
options = ChromiumOptions()
options.binary_location = '/path/to/your/chrome'  # Point to your Chrome
```

**Browser taking forever to start?**
```python
options.start_timeout = 30  # Give it more time (especially on slower machines)
```

**Need a proxy?**
```python
options.add_argument('--proxy-server=http://username:password@proxy:port')
```

**Running in Docker?**
```python
options.add_argument('--no-sandbox')
options.add_argument('--disable-dev-shm-usage')
```

**Permissions issues?**
```python
options.add_argument('--disable-web-security')
options.add_argument('--disable-features=VizDisplayCompositor')
```



## 📚 **Learn More**

Ready to become a Pydoll master? Our documentation has everything:

**[Complete Documentation](https://pydoll.tech/)** - Deep dives, tutorials, and examples  
**[API Reference](https://pydoll.tech/docs/api/)** - Every method, parameter, and return type  
**[Advanced Guides](https://pydoll.tech/docs/features/)** - Network interception, event handling, performance optimization  

*Chinese documentation available at [README_zh.md](README_zh.md)*

## 🤝 **Join the Revolution**

Love Pydoll? Help make it even better!

**🔥 Ways to contribute:**
- **Star the repo** (seriously, it means everything)
- **Report bugs** or suggest features  
- **Improve documentation**
- **Submit pull requests**
- **Share your success stories**

**Contributing Guidelines:**
- Write tests for new features
- Follow our code style (we use Ruff + MyPy)
- Use conventional commits
- Make sure CI passes

Check out [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide!


## 💖 **Support the Project**

Building and maintaining Pydoll takes time, coffee, and lots of love. If it's saving you hours of headaches:

**[Sponsor on GitHub](https://github.com/sponsors/thalissonvs)** - Get priority support and exclusive perks!

**Can't sponsor right now? No worries! You can still help:**
- ⭐ Star the repository  
- 🗣️ Tell your developer friends
- 📱 Share on social media
- ✍️ Write blog posts or tutorials
- 💬 Give feedback and report issues

**Every bit of support keeps this project alive and growing! 🚀**



## 🎊 **Spread the Word**

If Pydoll made your automation easier, help others discover it too!

Give it a ⭐, tell your colleagues, share it on social media, or write about your experience.


## 📄 **License**

Pydoll is MIT licensed - use it for anything! See [LICENSE](LICENSE) for details.

<div align="center">
  <h2><strong>Pydoll: Making Web Automation Simple and Powerful</strong></h2>
</div>
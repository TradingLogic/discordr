
# discordr

<!-- badges: start -->
[![Travis build status](https://travis-ci.org/EriqLaplus/discordr.svg?branch=master)](https://travis-ci.org/EriqLaplus/discordr)
[![Codecov test coverage](https://codecov.io/gh/EriqLaplus/discordr/branch/master/graph/badge.svg)](https://codecov.io/gh/EriqLaplus/discordr?branch=master)
<!-- badges: end -->

The goal of discordr is to make collaborating in Discord easier through a set of utility functions.

DiscordR uses the easy-to-use webhooks provided by Discord to interaction with channels. For more fine-grained control using websockets interacting directly with the Discord API, there is [another package](https://github.com/bill-ash/discoRd) which may be more appropriate.

## Installation

You can install the released version of discordr from GitHub with:

``` r
library(devtools)
install_github("EriqLaplus/discordr")
```

## Setup

This packages functions through Discord's easy-to-use webhook system. If you are the owner or administrator of a channel, you can setup a webhook by entering the channel settings (edit channel) and navigating to the webhook tab. If you are the participant of a channel, you may request a webhook from a server admin in order to use this package. While not required, it is recommended to set a default connection which consists of a username and webhook for easier use. If you use many webhooks in many different places, the connection objects make it mix and match. See documentation for programmatically setting a default environment webhook and username.

``` r
library(discordr)

conn_obj <- create_discord_connection(webhook = 'your-webhook-here.com', username = 'preferred username', set_default = TRUE)
```

## Examples

Once setup, there are five possible ways to interact with Discord through this package: sending messages, sending files, sending the current plot from RStudio, sending console output, sending r objects directly from RStudio, or even sending example compiled latex to others! For sending messages, use the `send_message` function with a character string. See package documentation if you are not setting a default username and/or default webhook

``` r
send_message("Hello World!")
```
For sending files, user the `send_file` function with the filepath as a character string.

``` r
send_file("hello_world.jpg")
send_file("updated_dataset.csv")
```

You can use the `send_plot_code` or `send_current_ggplot` functions to either compile and send a graphic or send the last plot shown in the Plots tab of RStudio. If using a ggplot workflow, using the appropriate `send_current_ggplot` function is recommended to obtain the highest image resolution.

``` r
send_current_ggplot()
```

Maybe you're interested in sharing some model output. You can send console output properly formatted with code syntax using the `send_console` function.

``` r
lm_model <- lm(x ~ y)
send_console(summary(lm_model))
```

You can bundle R objects you're working with into a single `RData` file to be sent to collaborators through the `send_robject` function.

``` r
x <- c(1,2,3,4,5)
y <- matrix(rep(0, 4), nrows = 2)
send_robject(x, y, filename = 'my_data.RData')
```

Maybe you're interested in running that latex model description past someone, you can do so using the `send_tex` function. I expect this functionality to be used only by a small fraction of users, and I would like to respect users who would prefer not to install many packages as dependences. If you would like to use this functionality, you will need to install the `texPreview` package manually.  

``` r
# use double slashes where you would normally use single slashes...
tex_string <- '$y_{ijk} = \\mu + \\alpha_i + \beta_j + \epsilon_{ijk}$'
send_tex(tex_string)
```

## Issues & Feedback

Please create an issue within this repository if you have any difficulty or error using the package. 

If you have suggestions, feedback, or raving reviews you would like to share, come talk to us [on Discord!](https://discord.gg/SAHPhZn)

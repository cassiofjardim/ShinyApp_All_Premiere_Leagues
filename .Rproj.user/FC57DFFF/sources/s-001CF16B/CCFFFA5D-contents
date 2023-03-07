library(shiny)
library(shinyWidgets)
library(tidyverse)
library(highcharter)
library(ggbump)
library(worldfootballR)


seasons_vector <- 2007:2022

leagues_seasons_list <- seasons_vector %>% map(
  ~ worldfootballR::fb_season_team_stats(
    country = 'ENG',
    gender = "M",
    season_end_year = .x,
    tier = '1st',
    stat_type = 'league_table'
  )
)

leagues_seasons_list <-
  leagues_seasons_list %>% set_names(seasons_vector)
squads_seasons <- list()
#
source(file = 'R/pie_chart_function.R')
source('R/modules/module_1_team_level.R')

path_clubs <- 'www/img/Premiere_League/'

ui <- fluidPage(tags$main(
  id  = 'main_page',

  #******************** Div 1 ******************************************************

  tags$div(
    id = "top",
    class = "top",
    tags$img(
      src = 'img/banner_2.png',
      class = 'banner',
      width = '100%',
      height = '100%'
    )

  ),
  #******************** Div 2 ******************************************************
  tags$div(
    id = "sidebar",
    class = "sidebar",

    radioGroupButtons(
      inputId = 'seasons',
      direction = 'vertical',
      justified = 'TRUE',
      size = 'sm',
      label = '',

      choices = sort(seasons_vector, decreasing = TRUE),
      selected = '2022'
    ),

    div(
      class = 'link_btn',

      htmlOutput('teams_icons'),
      verbatimTextOutput('print')
    )
  ),
  includeCSS(path = 'www/css/new_style.css'),


  div(
    class = 'main_grid_panel',
    #******************** TABSETPANELS ******************************************************

    tabsetPanel(
      tabPanel(
        title = tags$img(
          src = 'img/icons/stats.png',
          'Teams League Stats - Specifics',
          width = '24px',
          height = '24px'
        ),

        overview_mvp_UI('overview')
      ),
      #*****************************************************************************
      #****************************** Panel : Team Stats - Specifics*****************
      #*****************************************************************************

      tabPanel(
        title = tags$img(
          src = 'img/icons/stats.png',
          width = '24px',
          height = '24px',
          'Team Stats - Specifics'
        )

      ),
      #*****************************************************************************
      #****************************** Panel : Players Team Stats - Specifics*********
      #*****************************************************************************
      tabPanel(
        title = tags$img(
          src = 'img/icons/games.png',
          width = '24px',
          height = '24px',
          'Players Team Stats - Specifics'
        )
      ),
      #*****************************************************************************
      #****************************** Panel : Players Team Stats Comparision - All League Clubs***
      #*****************************************************************************
      tabPanel(
        title = tags$img(
          src = 'img/icons/stats.png',
          width = '24px',
          height = '24px',
          'Players Team Stats Comparision - All League Clubs'
        )
      ),

      #*****************************************************************************
      #****************************** Panel : Players Team Stats Comparision - All League Clubs***
      #*****************************************************************************
      tabPanel(
        title = tags$img(
          src = 'img/icons/stats.png',
          width = '24px',
          height = '24px',
          'Players Team - Video Analysis'
        )
      )
    )
  )
))



server <- function(input, output, session) {
  clubs_icons <-
    list.files(path = 'www/img/Premiere_League/') %>% sub(pattern = '.png',
                                                          replacement = '')

  output$teams_icons <- renderUI({
    leagues_seasons_list[[input$seasons]]$Squad %>%
      map(~ actionLink(
        inputId = paste0(.x),
        label =   tags$img(
          span(.x),
          src = paste0(
            sub(path_clubs, pattern = 'www/', replacement = ''),

            '/',
            .x,
            # if(FALSE){'others'}else{.x},
            '.png'
          ),
          style  = 'margin:0 .75em'
        )
      ))
  }) %>% bindCache(input$seasons)


  clubs_name <- reactiveValues()

  observe({
    clubs_name$team_1 <- leagues_seasons_list[[input$seasons]]$Squad[1]
  })


  observeEvent(input$seasons, {
    my_list <- leagues_seasons_list[[input$seasons]]$Squad
    n <- length(leagues_seasons_list[[input$seasons]]$Squad)
    lapply(1:n, function(i) {
      observeEvent(input[[my_list[i]]], {
        clubs_name$team_1 <- leagues_seasons_list[[input$seasons]]$Squad[i]
        clubs_name$team_1
      })
    })
  })

  overview_mvp_Server(
    'overview',
    season = reactive(input$seasons),
    clubs_name_input = reactive(clubs_name$team_1)
  )


}

shinyApp(ui, server)

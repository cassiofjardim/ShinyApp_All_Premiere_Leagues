overview_mvp_UI <- function(id) {
  ns <- NS(id)
  tagList(

    div(class = 'main_div_panel_1',
                div(
                  class = 'div_row_1_main',
                  div(
                    class = 'text_title',
                    div(style = 'display: flex; gap: 2em;',
                      htmlOutput(ns('name')),
                      highchartOutput(ns('chart1')),
                      highchartOutput(ns('chart2')),
                      highchartOutput(ns('chart3'))

                      ))
                ))
          )
}

overview_mvp_Server <- function(id, season,clubs_name_input) {
  moduleServer(id,
               function(input,
                        output,
                        session) {


                   output$chart1 <- renderHighchart({
                     # pie_chart_function(df = leagues_seasons_list[['2022']],
                     #                    x_axis = 'Squad', y_axis = 'xG',
                     #                    title_slice = 'Squad',
                     #                    slices_colors_list = list('red','green'))
                     })

                     output$chart2<- renderHighchart({
                     # pie_chart_function(df = leagues_seasons_list[[season()]],
                     #                    x_axis = 'Squad', y_axis = 'xG',
                     #                    title_slice = 'Squad',
                     #                    slices_colors_list = list('red','green'))
                       })

                     output$chart3 <- renderHighchart({
                     # pie_chart_function(df = leagues_seasons_list[[season()]],
                     #                    x_axis = 'Squad', y_axis = 'xG',
                     #                    title_slice = 'Squad',
                     #                    slices_colors_list = list('red','green'))
                                        })


output$name <- renderUI({

  tagList(
    h1(clubs_name_input()),

    h1('Temporada ',season()),

    # leagues_seasons_list[[print(season())]]%>%  pluck(1,1),



    # h1('Champion ', leagues_seasons_list[[paste0(season())]])
  )

})

})}



import plotly.graph_objects as go
import pandas as pd

# Dados
df = pd.DataFrame(dict(
    categorias=["Naturalmente ofensivo", "Naturalmente agradável", "Químico", "Terra", "Vegetal", "Culinário", "Marinho", "Animal", "Sabor", "Sensação"],
    Fossa=[29, 1, 4, 3, 0, 0, 1, 1, 0, 1], 
    ETEZR=[7, 4, 5, 12, 3, 1, 0, 6, 0, 2],
    ETE_Controle=[8, 0, 9, 16, 1, 1, 1, 3, 0, 1]
))

# Função para criar o gráfico
def create_polar_bar_chart(data, categorias, title, color):
    fig = go.Figure()
    fig.add_trace(go.Barpolar(
        r=data, 
        theta=categorias,
        marker=dict(color=color),
        opacity=0.8
    ))
    fig.update_layout(
        title=dict(
            text=title,
            x=0.5,  # Centraliza o título
            font=dict(size=20)
        ),
        polar=dict(
            radialaxis=dict(visible=True, showline=True, linewidth=2, gridcolor="lightgray"),
            angularaxis=dict(tickfont=dict(size=12)),
        ),
        height=600,
        width=600,
        showlegend=False
    )
    fig.update_polars(radialaxis=dict(range=[0, max(data) + 5], tickfont=dict(size=12), gridcolor="lightgray"))
    return fig

# Gráfico Polar Bar para Fossa
fig_fossa = create_polar_bar_chart(df["Fossa"], df["categorias"], "Gráfico Polar Bar - Fossa", "#63A644")
fig_fossa.show()

# Gráfico Polar Bar para ETEZR
fig_etezr = create_polar_bar_chart(df["ETEZR"], df["categorias"], "Gráfico Polar Bar - ETEZR", "#F2A649")
fig_etezr.show()

# Gráfico Polar Bar para ETE Controle
fig_controle = create_polar_bar_chart(df["ETE_Controle"], df["categorias"], "Gráfico Polar Bar - ETE Controle", "#0A0240")
fig_controle.show()

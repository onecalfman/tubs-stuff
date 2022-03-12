---
documentclass: article
classoption:
 - twocolumn
title: Ökonometrie Zusammenfassung
author: Jonas Walkling
lang: de
geometry:
  - paperheight=297mm
  - paperwidth=210mm
  - top=20mm
  - left=10mm
  - right=10mm
  - bottom=20mm
tables-no-page-break: true
disable-header-and-footer: true
header-includes:
  - \usepackage[T1]{fontenc}
  - \usepackage{tikz}
  - \usetikzlibrary{calc}
  - \usetikzlibrary{arrows,decorations.markings}
  - \usepackage{svg}
  - \usepackage{booktabs}
  - \usepackage{makecell}
  - \usepackage{wrapfig}
  - \usepackage{float}
  - \setcounter{secnumdepth}{3}
  - \setcounter{tocdepth}{4}
  - \newcommand{\var}{\operatorname{var}}
  - \newcommand{\cov}{\operatorname{cov}}
---

# Definitionen

Mittelwert
: $\displaystyle \bar{x}=\frac{1}{n} \sum_{i=1}^{n} x_{i}$

Varianz
: $\displaystyle \operatorname{VAR}(x) = s_{x}^{2}=\frac{1}{n-1} \sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}$

Covarianz
: $\displaystyle \operatorname{COV}(x,y) = c_{x y}$\
  $=\frac{1}{n-1} \sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)\left(y_{i}-\bar{y}\right)$

Sample Regression Function
: $\displaystyle \hat{y}=b_{1}+b_{2} x$

Fittet Values / Vorhersage
: $\displaystyle \hat{y}_{i}=b_{1}+b_{2} x_{i}$

Residual
: $\displaystyle \hat{u}_{i}=y_{i}-\hat{y}_{i}$

Fehlerterm
: $u_{i} = y_{i}-E\left(y_i \mid x_{i}\right)$

Bestimmtheitsmaß
: $\displaystyle R^{2}=\frac{\var(\hat{y})}{\var(y)}=1-\frac{\var(\hat{u})}{\var(y)}$

Geschätzter Standardfehler:
: $\hat{\sigma}_{b_{k}}=\sqrt{\operatorname{var}\left(b_{k}\right)}$


# OLS

## Herleitungen der Parameter

### Momentenmethode
\begin{align*}
u&=y-\beta_{1}-\beta_{2} x \\
E(u) &= \mathrm{E}\left(y-\beta_{1}-\beta_{2} x\right) = 0  \\
& \Rightarrow \frac{1}{n} \sum\left(y_{i}-b_{1}-b_{2} x_{i}\right)=0 \\
\mathrm{E}(x \cdot u) &= E\left[x \cdot\left(y-\beta_{1}-\beta_{2} x\right)\right] =0\\
& \Rightarrow \frac{1}{n} \sum\left[x_{i} \cdot\left(y_{i}-b_{1}-b_{2} x_{i}\right)\right]=0\\
\\
b_{1} &=\bar{y}-b_{2} \bar{x} \\
b_{2} &=\frac{\sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)\left(y_{i}-\bar{y}\right)}{\sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}} =\frac{S_{x y}}{S_{x}^{2}}
\end{align*}

### Minimierungsproblem \

$\displaystyle \min_{b_{1}, b_{2}} \sum_{i=1}^{N} \hat{e}_{i}^{2}=\min _{b_{1}, b_{2}} \sum_{i=1}^{N}\left(y_{i}-b_{1}-b_{2} x_{i}\right)^{2}$

\begin{align*}
\frac{\partial \sum \hat{e}^2}{\partial b_1} & = -2 \sum \hat{e} = 0   \\
& \Rightarrow \sum_N (y - b_1 - b_2 x ) = 0 \\
& \Leftrightarrow \sum y = \sum b_1 + b_2 \sum x \\
& \Leftrightarrow \bar{y} N = N b_1 + b_2 \sum \bar{x} N \\
& \Leftrightarrow b_1 = \bar{y} - b_2 \bar{x} \\
\\
\frac{\partial \sum \hat{e}^2}{\partial b_2} & = -2 \sum \hat{e} x = 0 \\
& \Rightarrow \sum\left(y-b_{1}-b_{2} x\right) x=0 \\
& \Leftrightarrow \sum\left(y-\left(\bar{y}-b_{2} \bar{x}\right)-b_{2} x\right) x=0 \\
& \Leftrightarrow \sum \left(y-\bar{y}-b_{2}(x-\bar{x})\right) x=0 \\
& \Leftrightarrow \sum(y-\bar{y})_{x}=b_{2} \sum(x-\bar{x}) x \\
& \Leftrightarrow  b_2 = \frac{\sum(x-\bar{x})(y-\bar{y})}{\sum(x-\bar{x})^{2}} =\frac{S_{x y}}{S_{x}^{2}}
\end{align*}

Substitutionen:
\begin{align*}
\bar{x} & = \frac{1}{N} \sum_N x \\
\bar{x} N & = \sum_N x\\
\sum (x-\bar{x}) x & = \sum (x-\bar{x})^{2} \\
\sum(y-\bar{y})x & =\sum(y-y)(x-\bar{x})
\end{align*}

## Annahmen OLS{#Annahmen}

1. Linearität von $y=\beta_{2}+\beta_{2} x+e$
2. Stichprobenvarianz
3. Zufallsstichprobe ^[Impliziert das eine unabhängige und identische Verteilung vorliegt (independet and identical distribution (iid)). Bei beobachteten Daten ist diese Annahme sehr Kritisch. Hier lässt sich nicht sicherstellen das der datangenerierende Prozess wirklich zufällig ist.] $\left(x_{i}, y_{i}\right)$ ist unabhängig von $\left(x_{j}, y_{j}\right)$ 
4. Konditionaler Erwartungswert = 0 = $E(e \mid x)$
5. Homoskedastizität $\var\left(e_{i} \mid X_{i}\right)=\sigma^{2}$
6. Die Verteilung des Störterms, konditional auf $x_i$, ist normal: $e_{i} \mid x_{i} \sim \mathcal{N}\left(0, \sigma^{2}\right)$

## Eigenschaften OLS

1. Summe der OLS-Residuen = 0\
   $\sum_{i} \hat{e}_{i}=\overline{\hat{e}}=0$
2. gefitterer Mittelwert = beobachteter Mittelwert 
   $$\begin{aligned}\\&\hat{e}_{i}=y_{i}-\hat{y}_{i} \rightarrow \sum_{i} \hat{e}_{i}=\sum_{i} y_{i}-\sum_{i} \hat{y}_{i}\\&\frac{1}{N} \sum_{i} \hat{e}_{i}=\frac{1}{N} \sum_{i} y_{i}-\frac{1}{N} \sum_{i} \hat{y}_{i}\\&\overline{\hat{e}}=\bar{y}-\overline{\hat{y}}=0 \quad \text { wenn } \quad \overline{\hat{e}}=0 \text { (siehe 1.) gilt weiter }\\&\overline{\hat{y}}=\bar{y}\\\end{aligned}$$
   (gilt nur mit Interzept)

3. $\sum_{i} \hat{e}_{i} x_{i}=0 \vee \operatorname{cov}\left(x_{i}, \hat{e}_{i}\right)=0$
   $$\begin{array}{l}\\\sum_{i}\left(x_{i}-\bar{x}\right)\left(\hat{e}_{i}-\overline{\hat{e}}\right)=\sum_{i} x_{i} \hat{e}_{i}-\bar{x} \sum_{i} \hat{e}_{i}=0 \quad \text { wenn } \\\\\sum_{i} \hat{e}_{i}=\overline{\hat{e}}=0\\\end{array}$$

4. $\operatorname{cov}\left(\hat{y}_{i}, \hat{e}_{i}\right)=0$
   $$\begin{aligned}
   \operatorname{cov}\left(\hat{y}_{i}, \hat{e}_{i}\right)&=\operatorname{cov}\left(\left[b_{1}+b_{2} x_{i}\right], \hat{e}_{i}\right)\\
   & =\operatorname{cov}\left(b_{1}, \hat{e}_{i}\right)+\operatorname{cov}\left(b_{2} x_{i}, \hat{e}_{i}\right) \\
   & =0+b_{2} \operatorname{cov}\left(x_{i}, \hat{e}_{i}\right)\\
   & =0
   \end{aligned}$$
   (mit Interzept)

## Qualität OLS
Der OLS-Schätzer liefert für verschiedene Stichproben verschieden Werte. Die Schätzer selbst sind damit Zufallsvariablen.

### Eigenschafen

- Erwartungstreue
  $$E\left[b_{2}\right]=\beta_{2}$$
- Effizienz (Geringe Stichprobenvariation)
  $$\var\left[b_{2}\right]<\var\left[b_{2}^{*}\right]$$
- Konsistenz (Ein Schätzer wird mit zunehmender Stichprobengröße genauer)
  $$\lim_{N \rightarrow \infty} P\left[\left|b_{N}-\beta\right|<\delta\right]=1 \quad \delta>0$$

### Unverzerrtheit

Erwartungstreue/Unverzerrtheit
: $E(\hat{\theta})=\theta$

Konsistenz
: $\var(\hat{\theta}) \rightarrow 0, \quad \text{für} \quad n \rightarrow \infty$

#### Relation zwischen $\beta_2$ und $b_2$ herstellen
$$\begin{aligned}
b_{2} &=\frac{\sum_{i}\left(x_{i}-\bar{x}\right)\left(y_{i}-\bar{y}\right)}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}} \\
 &=\frac{\sum_{i}\left(x_{i}-\bar{x}\right)\left(\beta_{1}+\beta_{2} x_{i}+e_{i}-\beta_{1}-\beta_{2} \bar{x}-\bar{e}\right)}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}}\\
 &=\frac{\sum_{i}\left(x_{i}-\bar{x}\right) \beta_{2}\left(x_{i}-\bar{x}\right)}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}}+\frac{\sum_{i}\left(x_{i}-\bar{x}\right)\left(e_{i}-\bar{e}\right)}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}} \\
 &=\beta_{2}+\frac{\sum_{i}\left(x_{i}-\bar{x}\right)\left(e_{i}-\bar{e}\right)}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}}
\end{aligned}$$

##### Substitutionen:
\begin{align*}
\sum \left(x_{i}-\bar{x}\right)&=0\\
\sum x_i-n \cdot \bar{x}&=0
\end{align*}

#### Erwartungswert Bilden
$$\begin{aligned} E\left(b_{2}\right) &=\beta_{2}+\sum_{i} E\left(\frac{\left(x_{i}-\bar{x}\right)\left(e_{i}-\bar{e}\right)}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}}\right) \\
&=\beta_{2}+\sum_{i} \frac{E\left(\left(x_{i}-\bar{x}\right)\left(e_{i}-0\right)\right)}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}} \\
&=\beta_{2}+\sum_{i} \frac{E(cov(x_i,e_i))}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}}
\end{aligned}$$

#### Unverzerrtheit von $b_1$\
Unter der Annahme, dass $b_2$ unverzerrt ist gilt:
$$E\left(b_{1}\right)=E\left(\left[\beta_{1}+\beta_{2} \bar{X}\right]-b_{2} \bar{X}\right)=\beta_{1}$$


#### Beispiel

$$T_{1}=\bar{X}, \quad X \sim \mathcal{N}\left(\mu, \sigma^{2}\right), \quad E(X)=\mu, \quad \var(X)=\sigma^{2}$$
\begin{align*}
E\left(T_{1}\right)&=E(\bar{X})=E\left(\frac{1}{n} \sum_{i=1}^{n} X_{i}\right) \\
&=\frac{1}{n} \sum_{i=1}^{n} E\left(X_{i}\right) \\
&=\frac{1}{n} \sum_{i=1}^{n} \mu=\frac{1}{n} n \mu=\mu \\
\\
\var\left(T_{1}\right)&=\var(\bar{X})=\var\left(\frac{1}{n} \sum_{i=1}^{n} X_{i}\right) \\
 &=\frac{1}{n^{2}} \sum_{i=1}^{n} \var\left(X_{i}\right) \\
 &=\frac{1}{n^{2}} \sum_{i=1}^{n} \sigma^{2}=\frac{1}{n^{2}} n \sigma^{2}=\frac{\sigma^{2}}{n} \rightarrow 0
\end{align*}

### Varianz und Kovarianz von OLS

\begin{align*}
\var (b_{1}) &=E\left(\left[b_{1}-E\left(b_{1}\right)\right]^{2}\right)=\sigma^{2}\left[\frac{\sum_{i} x_{i}^{2}}{N \sum_{i}\left(x_{i}-\bar{x}\right)^{2}}\right]\\
\var (b_2) &=\frac{\sigma^{2}}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}}\\
\operatorname{cov}\left(b_{1}, b_{2}\right) &=E\left(\left[b_{1}-E\left(b_{1}\right)\right]\left[b_{2}-E\left(b_{2}\right)\right]\right) \\
&=E\left(\left[b_{1}-\beta_{1}\right]\left[b_{2}-\beta_{2}\right]\right) \\
& =-\bar{x} E\left(\left[b_{2}-\beta_{2}\right]^{2}\right) \\
\cov (b_{1}, b_{2}) &= -\bar{x} \operatorname{var}\left(b_{2}\right)
\end{align*}

#### Hereitung $\var(b_2)$

\begin{align*}
b_{2}&=\beta_{2}+\frac{\sum_{i}\left(x_{i}-\bar{x}\right) e_{i}}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}}\\
b_2 & = \beta_{2}+\frac{1}{\sum \left(x_{i}-\bar{x}\right)^{2}} \sum\left(x_{i}-\bar{x}\right) e_{i}\\
\var &  = \var \left(\beta_{2}\right)+\var \left(\frac{1}{\sum (1-\bar{x})^{2}}\sum \left(x_{i}-\bar{x}\right)_{e_{i}}\right)\\
& = \left(\frac{1}{\sum\left(x_{1}-\bar{x}\right)}^{2}\right)^{2} \var\left(\sum\left(x_{i}-\bar{x}\right) e_{i}\right)\\
\var\left(b_{2}\right)&=\frac{\sum_{i}\left(x_{i}-\bar{x}\right)^{2} \var\left(e_{i}\right)}{\left(\sum_{i}\left(x_{i}-\bar{x}\right)^{2}\right)^{2}}\\
\var (b_2) &=\frac{\sigma^{2}}{\sum_{i}\left(x_{i}-\bar{x}\right)^{2}}
\end{align*}

#### Substitutionen:
\begin{align*}
\var(ax) &= a^2 \var(x)\\
\var (a x+b y) &=a^{2} \var (x)+ b^{2} \var (y)+ 2 a b \operatorname{cov}(x, y)\\
\end{align*}

### Schätzer $\; \hat{\sigma}^2$
\begin{align*}
\sigma^{2} &=\frac{E\left[\sum_{i} \hat{e}_{i}^{2}\right]}{N-2}\\
\hat{\sigma}^{2} &=\frac{\sum_{i} \hat{e}_{i}^{2}}{N-2}\\
\hat{\sigma}^{2} &=\frac{\sum_{i} \hat{e}_{i}^{2}}{N-K} \leftarrow \text{für K Parameter}\\
\\
\hat{\sigma}&=\sqrt{\frac{\sum_{i} \hat{e}_{i}^{2}}{N-K}}\\
\end{align*}

## Bestimmtheitsmaß $R^2$
$$R^{2}=\frac{E S S}{T S S}=1-\frac{S S R}{T S S}$$

### Herleitung
\begin{align*}
y_{i}&=\hat{y}_{i}+\hat{e}_{i}\\
\var(y) &=\operatorname{var}(\hat{y})+\operatorname{var}(\hat{e})+2 \operatorname{cov}(\hat{y}, \hat{e}) \\
 &=\operatorname{var}(\hat{y})+\operatorname{var}(\hat{e})\\
\frac{1}{N} \sum_{i=1}^{N}\left(y_{i}-\bar{y}\right)^{2} &=\frac{1}{N} \sum_{i=1}^{N}\left(\hat{y}_{i}-\overline{\hat{y}}\right)^{2}+\frac{1}{N} \sum_{i=1}^{N}\left(\hat{e}_{i}-\overline{\hat{e}}\right)^{2} \\ \underbrace{\sum_{i=1}^{N}\left(y_{i}-\bar{y}\right)^{2}}_{\text {TSS \tiny total sum of squares }} &=\underbrace{\sum_{i=1}^{N}\left(\hat{y}_{i}-\overline{\hat{y}}\right)^{2}}_{\text {ESS \tiny explained sum squared}}+\underbrace{\sum_{i=1}^{N}\left(\hat{e}_{i}-\overline{\hat{e}}\right)^{2}}_{\text {SSR \tiny sum of squard residuals}}
\end{align*}

## Gauss-Markov-Theorem
> Unter den [Gauss'schen Annahmen](#Annahmen) des klassischen lineare Regressionsmodells hat der OLS-Schätzer innerhalb der Klasse aller linearen und erwartungstreuen Schätzfunktionen die leinste Varianz, oder in anderen Worten, er ist BLUE d.h. ein **B**est **L**inear **U**nbiased **E**stimator.

## Asymptotische Eigenschaften 
Untersuchen das Verhalten von Zufallsvariablen die gegen $\infty ( \approx 150)$ gehen.

### Konsistenz
>$b_{N}$ ist eine konsistente Schätzfunktion für $\beta$ wenn gilt:
>$$\lim_{N \rightarrow \infty} P\left[\left|b_{N} - \beta\right|<\delta\right]=1 \quad \delta>0$$
>das heißt, dass die Wahrscheinlichkeit $(P)$, dass mit steigendem Stichprobenumfang der Absolutbetrag der Differenz zwischen $b_{N}$ und $\beta$ kleiner als eine beliebig kleine Zahl $\delta$ wird, gegen $1$ konvergiert.

### Asymptotische Normalverteilung
Schätzer aus einer Grundgesamtheit konvergieren bei genügend Stichproben gegen Normalverteilung. Egal, ob die Grundgesamtheit normalverteilt ist oder nicht.

### Asymptotische Effizienz

- $b$ sei ein Schätzer für $\beta$.
- Die Varianz der asymptotischen Verteilung von $b$ heißt asymptotische Varianz von $b$.
- Wenn $b$ konsistent ist und die asymptotische Varianz kleiner ist als die aller anderen konsistenten Schätzer, dann heißt $b$ asymptotisch effizient.

# Intervallschätzung und Hypothesentests
Annahmen über die Verteilung des Fehlerterms.
Die Annahme 6. der Gauss'schen Annahmen sorgt dafür, dass der OLS Schätzer die kleinste Varianz innerhalb der unverzerrten Schätzer besitzt.
Die Annahme ist nicht kritisch, da der Schätzer asymptotisch gegen die Normalverteilung strebt.

## Intervalschätzer

### Schritte

1. Berechnung des Punktschätzers $b_k$ und eines Schätzers $\hat{\sigma}^2$
2. Festlegung von $\alpha$ und bestimmen von $t_{\alpha / 2}^{c}$ mit $N-K$ Freiheitsgraden
3. Berechnung des Intervalschätzers $$P\left[b_{k}-t_{\alpha / 2}^{c} \hat{\sigma}_{b_{k}} \leq \beta_{k} \leq b_{k}+t_{\alpha / 2}^{c} \hat{\sigma}_{b_{k}}\right]=1-\alpha$$
4. Interpretation des Intervalschätzers: $(1-\alpha) \times 100 \%$ der Konfidenzintervalle enthalten $\beta$

##### Konfidenzintervalle sind enger wenn:

- je größer $\alpha$
- je kleiner $\sigma^2$
- je größer $N$


#### Standardfehler
\begin{align*}
\operatorname{var}\left(e_{i}\right)& \equiv \sigma^{2}\\
\operatorname{var}\left(b_{2}\right)&=\sigma_{b_{2}}^{2}=\sigma^{2} / \sum_{i}\left(x_{i}-\bar{x}\right)^{2}
\end{align*}


Punktschätzer
: dienen zur Schätzung eines unbekannten Parameters einer Grundgesamtheit auf grundlage einer Einyelnen Stichprobe. Vermitteln allerdings keine Informationen über die Unsicherheit.

### Normalverteilung

\begin{align*}
P & [z \leq-1.96]=P[z \geqslant+1,96]=0.025\\
P & [-1.96 \leq z \leq+1.96]=1-0.05=0.95\\
P & \left[-1.96 \leq \frac{b_{k}-\beta_{k}}{\sigma_{b_{k}}} \leq+1.96\right]=0.95\\
P & \left[-z_{\alpha / 2} \leq \frac{b_{k}-\beta_{k}}{\sigma_{b_{k}}} \leq+z_{\alpha / 2}\right]=1-\alpha\\
\end{align*}

### T-Verteilung

> Der Wert der ausgegenenen t-Statistik ist einfach Koeffizient dividiert durch Stadardfehler: $$t-Stat(b_k) = \frac{b_k}{\hat{\sigma}}_{b_k}$$

\begin{align*}
P & \left[-t_{\alpha / 2}^{c} \leq \frac{b_{k}-\beta_{k}}{\hat{\sigma}_{b_{k}}} \leq+t_{\alpha / 2}^{c}\right]=1-\alpha\\
P & \left[b_{k}-t_{\alpha / 2}^{c} \hat{\sigma}_{b_{k}} \leq \beta_{k} \leq b_{k}+t_{\alpha / 2}^{c} \hat{\sigma}_{b_{k}}\right]=1-\alpha
\end{align*}

\begin{align*}
H_{0}: \mu & =    \mu_0, \quad H_{1}: \mu \neq \mu_0 \\
H_{0}: \mu & \geq \mu_0, \quad H_{1}: \mu <    \mu_0 \\
H_{0}: \mu & \leq \mu_0, \quad H_{1}: \mu >    \mu_0 \\
\end{align*}

## Einfache Hypothesentests

1. Ausgangssituation: Formuliere die Annahmen und nicht zu testenden Hintergrundhypothesen (z.B. b ist normalverteilt mit ...)
1. Formuliere die Alternativ- und Nullhypothese z.B. $H_{1}: \beta = 0, H_{0}: \beta=0$
1. Wähle die Teststatistik (z.B. t-Stat $=b / \hat{\sigma}_{b})$
1. Bestimme die Verteilung der Teststatistik unter der Annahme, dass die Nullhypothese gilt z.B. $b / \hat{\sigma}_{b} \sim t_{N-2}$.
1. Wähle das Signifikanzniveau und bestimme den Annahme- und Verwerfungsbereich (z.B. behalte die Nullhypothese wenn $-1.96 \leq b / \hat{\sigma}_{b} \leq+1.96$ ; anderenfalls verwirf die Nullhypothese).

## Zweiseitige Hypothesentests
\begin{align*}
P&\left[\beta^{0}-t_{\alpha / 2}^{c} \hat{\sigma}_{b} \leqslant b \leqslant \beta^{0}+t_{\alpha / 2}^{c} \hat{\sigma}_{b}\right]=1-\alpha\\
&\left[\beta^{0}-t_{\alpha / 2}^{c} \hat{\sigma}_{b} ; \beta^{0}+t_{\alpha / 2}^{c} \hat{\sigma}_{b}\right]
\end{align*}


## Fehlerarten
1. Fehler 1. Art: Nullhypothese wird fälschlicherweise Verworfen
2. Fehler 2. Art: Nullhypothese wird fälschlicherweise Aktzeptiert




# Logarithmen

\begin{align*}
y&=a \cdot x^{\beta_{2}} \cdot v\\
\log (y)&=\log \left(a \cdot x^{\beta_{2}} \cdot v\right)=\underbrace{\log (a)}_{\beta_{1}}+\beta_{2} \cdot \log (x)+\underbrace{\log (v)}_{u} \\
\Rightarrow \log (y)&=\beta_{1}+\beta_{2} \log (x)+u\\
\\
\frac{\partial y}{\partial x}&=\beta_{2} \frac{y}{x} \quad \Leftrightarrow \quad \beta_{2}=\frac{\partial y}{\partial x} \frac{x}{y}\\
\end{align*}

$$
\begin{array}{lllrl}
\text { Level-level } & y        & x        & \Delta    y= & \beta_{2} \Delta x \\
\text { Level-log }   & y        & \log (x) & \Delta    y= & \left(\beta_{2} / 100\right) \% \Delta x \\
\text { Log-level }   & \log (y) & x        & \% \Delta y= & \left(100 \beta_{2}\right) \Delta x \\
\text { Log-log }     & \log (y) & \log (x) & \% \Delta y= & \beta_{2} \% \Delta x
\end{array}$$


# Multivariates Modell
Die Annahme, dass alle Variablen gleich und unabhängig Verteilt sind ist bei realen Daten oft nicht gegeben. Variablen können sich statistisch beeinflussen, ohne das ein kausaler Zusammenhang besteht.

## Heteroskedastizität
> Ungleiche Varianz der Störterme.

Die Varianz der einzelnen Fehlerterme ist definiert als:
$$\var(e_i) = \sigma_i^2$$

Die Annahmen $e_i \sim iid(0,\sigma_i^2), \quad E(e_i)=0 \quad \text{und} \quad \cov(e_i,e_j) = 0 \:$ gelten weiterhin.

Der OLS-Schätzer bleibt erwartungstreu und konsitent.

### Maßnahmen gegen Heteroskedastizität 
- Heteroskedastiekonsistente Standardfehler
  - $\displaystyle \var(b_2) = \sum_i^N \frac{(x_i-\bar{x})^2 \sigma_i^2}{\left(\sum_i^N ( x_i- \bar{x})^2\right)^2}$
- weighted - generalized Least Squares (WLS and GLS)

<!--
### Regression auf Konstante

\begin{align*}
y &=\beta_{1}+u\\
\beta_0 &= \bar{y}
\end{align*}

### Regression ohne Konstante
$$y=\beta_{2} x+u$$


### Multiple Regression
$$y=\beta_{1}+\beta_{2} x_{2}+\beta_{2} x_{2}+\cdots+\beta_{k} x_{k}+u$$
$$\underset{1 \times(k+1)}{\mathbf{x}_{i}}=\left[\begin{array}{lllll}1 & x_{i 1} & x_{i 2} & \ldots & x_{i k}\end{array}\right], \quad \underset{(k+1) \times 1}{\boldsymbol{\beta}}=\left[\begin{array}{c}\beta_{1} \\ \beta_{2} \\ \vdots \\ \beta_{k}\end{array}\right]$$



$$y_{i}=\vec{x}_{i} \vec{\beta}+u_{i}$$

\begin{align*}
\mathbf{y}_{n \times 1}&=\left[\begin{array}{c}y_{2} \\ y_{2} \\ \vdots \\ y_{n}\end{array}\right], \quad \underset{n \times 1}{\mathbf{u}}=\left[\begin{array}{c}u_{2} \\ u_{2} \\ \vdots \\ u_{n}\end{array}\right] \\ 
\underset{n \times(k+1)}{\mathbf{X}}&=\left[\begin{array}{c}\mathbf{x}_{2} \\ \mathbf{x}_{2} \\ \vdots \\ \mathbf{x}_{n}\end{array}\right]=\left[\begin{array}{cccc}1 & x_{11} & \cdots & x_{1 k} \\ 1 & x_{21} & \cdots & x_{2 k} \\ \vdots & \vdots & \ddots & \vdots \\ 1 & x_{n 1} & \cdots & x_{n k}\end{array}\right]
\end{align*}
\begin{align*}
\underset{n \times 1}{\mathbf{y}}&=\underbrace{\mathbf{X} \boldsymbol{\beta}}_{n \times 1}+\underset{n \times 1}{\mathbf{u}}\\
\hat{\boldsymbol{\beta}}&=\left(\mathbf{X}^{\prime} \mathbf{X}\right)^{-1} \mathbf{X}^{\prime} \mathbf{y}
\end{align*}
-->

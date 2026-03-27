# 本科模板使用说明

**适用范围**
本说明面向本科毕业论文与本科开题/中期报告。

**首次准备**
1. 在仓库根目录运行 `xelatex heuthesis.ins` 生成 `heuthesisbook.cls` 与 `heuthesisart.cls`。
2. Windows 建议使用 `fontset=windows`，其他系统字体配置见 `README.md`。

**本科中期报告**
主文件：`examples/art/reports/report.tex`  
封面信息：`examples/art/reports/front/coverart.tex`  
正文：`examples/art/reports/body/bachelor_midterm.tex`

配置入口：
`examples/art/reports/report.tex` 中的 `\documentclass[...]`。

可配置项：
- `type=bachelor`
- `stage=midterm`
- `fontset=windows|fandol|mac|ubuntu|adobe`
- `campus=harbin|qingdao|yantai`
- `toc=true|false`

编译流程（不使用 `make` 时）：
```bash
xelatex report.tex
bibtex report
xelatex report.tex
xelatex report.tex
```

**本科毕业论文**
主文件：`examples/book/bachelor/main.tex`  
封面与摘要：`examples/book/bachelor/front/cover.tex`  
正文章节：`examples/book/bachelor/body/chap01.tex` 等  
结论与附录：`examples/book/bachelor/back/conclusion.tex`、`examples/book/bachelor/back/AppendixA.tex` 等  
参考文献：`examples/book/bachelor/reference.bib`

配置入口：
`examples/book/bachelor/main.tex` 中的 `\documentclass[...]`。

可配置项：
- `type=bachelor`
- `fontset=windows|fandol|mac|ubuntu|adobe`
- `tocfour=true|false`
- `subtitle=true|false`
- `openright=true|false`
- `pageempty=true|false`
- `engtoc=true|false`
- `campus=harbin|qingdao|yantai`
- `library=true|false`

封面字段位置：
`examples/book/bachelor/front/cover.tex` 中的 `\heusetup{...}`。

常用字段：
- `statesecrets`、`cnumber`、`natclassifiedindex`、`intclassifiedindex`
- `ctitlecover`、`ctitle`
- `csubject`、`caffil`、`cauthor`
- `csupervisor`、`cprofessional`、`csupervisorcaffil`
- `csubmitdate`、`coralexdate`、`cstudentid`、`cdate`
- `etitle`、`ckeywords`、`ekeywords`

原创性声明页：
`examples/book/bachelor/main.tex` 中的 `\authorization[auscan.pdf]` 可替换为你的扫描件文件名，
或改用 `\authorization` 生成模板页。

目录与图表清单：
在 `examples/book/bachelor/main.tex` 中取消注释 `\listoffigures`、`\listoftables` 即可生成对应清单。

编译流程（不使用 `make` 时）：
```bash
xelatex main.tex
bibtex main
xelatex main.tex
xelatex main.tex
```

**写作流程建议**
1. 完成封面与摘要：编辑 `examples/book/bachelor/front/cover.tex` 与 `examples/art/reports/front/coverart.tex`。
2. 编写正文：在 `examples/book/bachelor/body/` 与 `examples/art/reports/body/` 中维护内容文件。
3. 维护参考文献：在 `examples/book/bachelor/reference.bib` 中添加条目，并在正文中 `\cite{}` 引用。
4. 插入图片：统一放到 `figures/` 目录，通过 `\includegraphics` 引用。
5. 编译检查：优先使用示例目录下的 `build.bat` 或按上面的手动流程编译。

**CI 自动编译（GitHub Actions）**
1. CI 使用 Linux 环境，建议在主文件中保持 `fontset=fandol`。
2. CI 需要先运行 `xelatex heuthesis.ins` 生成 `heuthesisbook.cls` 和 `heuthesisart.cls`。
3. 本仓库的示例流程已在 `.github/workflows/compile.yml` 中配置。
4. 流程内容包含：生成类文件，编译本科论文 `examples/book/bachelor/main.tex`，编译本科中期报告 `examples/art/reports/report.tex`，上传 PDF 为 Artifact，并在 tag 推送时发布 Release。

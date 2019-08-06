# coding=utf-8
from PyPDF2 import PdfFileReader, PdfFileWriter
from tkinter.filedialog import *

info = {
    'path':[]
}
def make_app():
    app = Tk()
    Label(app, text='懒人找资源pdf合成', font=('Hack',20,'bold')).pack()  #Hack是自己安装的字体，如果你没安装，可以用系统自带的Arial字体
    Listbox(app, name='lbox', bg='#778899').pack(fill=BOTH, expand=True)
    Button(app, text='open', command=ui_getdata).pack()
    Button(app, text='compresss', command=compress).pack()
    app.geometry('300x400')
    return app

def ui_getdata():
    f_names = askopenfilenames()
    lbox = app.children['lbox']
    info['path'] = f_names
    if info['path']:
        for name in f_names:
            lbox.insert(END, name.split('/')[-1])
        # abc.jpg
def compress():
    pdf_writer = PdfFileWriter()
    outputPages = 0
    paths = info['path']
    try:
        output = "合成" + paths[0].split('/')[-1].split('-')[0] + '.pdf'
    except:
        output = '合成.pdf'
    for path in paths:
        pdf_reader = PdfFileReader(path)
        pageCount = pdf_reader.getNumPages()
        for page in range(pdf_reader.getNumPages()):
            # 将每页添加到writer对象
            pdf_writer.addPage(pdf_reader.getPage(page))
        path_name = path.split('/')[-1].replace('.pdf', '')
        # print(path_name)
        try:
            title=path_name.split('-')[0]
            bookmark = path_name.replace(title+"- ","")
        except:
            bookmark = path_name

        pdf_writer.addBookmark(
            title=bookmark, pagenum=outputPages - pageCount
        )
    # 写入合并的pdf
    with open(output, 'wb') as out:
        pdf_writer.write(out)

app = make_app()
app.mainloop()


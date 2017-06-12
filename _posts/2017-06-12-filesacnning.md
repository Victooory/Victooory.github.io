---
layout: post
title: 文件扫描器
bigimg: /img/filescanning.png
---



**功能**：计算指定目录下的文件大小，并把显示后的内容保存到文本中<br>

**可扩展**：

 - 把io和读取目录再分离方便进行其他扩展
 - 增加对目录下的查询功能
 - 目录太大扫描会很久，可增加目录输出与扫描并行，加快速度

目录结构

    public class Directory {
	    private String name; // 名字
	    private long size; // 大小
	    private Set<Directory> son; // 子目录
	    private PrintWriter out;
	    ...
	    }
	    
添加子目录

    public Directory addDirectory(String name) {
		Directory directory = new Directory(name);
		son.add(directory);
		return directory;
	}
	
目录输出

    public void showDir(Directory directory) { // 先判断有无文件
		try {
			out = new PrintWriter(new FileOutputStream("C:\\zWork\\Workspaces\\jee\\test\\src\\result.txt"), true);
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		};
		this.showDir(1, directory); // 显示目录的方法
	}

	public void showDir(int indent, Directory directory) {
		for (int i = 0; i < indent; i++)
			out.print(" ");
		out.print("|");
		for (int i = 0; i < indent / 4; i++)
			out.print("—");
		out.println(directory.getStrOfDir());
		if (directory.isDirectory()) {
			Iterator<Directory> it = directory.getSon().iterator(); // son
			while (it.hasNext())
				showDir(indent + 4, it.next());
		}
	}
	
格式化输出目录

    public String getStrOfDir() {
		int size;
		String rst;
		if (this.getSize() < 1024) {
			rst = new String(this.getName() + " (" + this.getSize() + "B)");
		} else if (this.getSize() < 1024 * 1024) {
			rst = new String(this.getName() + " (" + this.getSize() / 1024 + "KB)");
		} else if (this.getSize() < 1024 * 1024 * 1024) {
			rst = new String(this.getName() + " ("
					+ new DecimalFormat("0.00").format((double) (this.getSize() / 1024) / 1024) + "MB)");
		} else {
			rst = new String(this.getName() + " ("
					+ new DecimalFormat("0.00").format((double) (this.getSize() / 1024 / 1024) / 1024) + "GB)");
		}
		return rst;
	}
	
扫描指定file下的目录

    public long ScanningAll(Directory directory,File F){			
		long size = 0;	
		File[] files = F.listFiles();
		if (files != null) {
			for (File file : files) {
				long cursize = 0;
				Directory son = directory.addDirectory(file.getName());
				if (file.isDirectory()) {
					cursize = this.ScanningAll(son,file);
				} else {
					cursize = file.length();
				}
				size +=cursize;
				son.setSize(cursize);
			}
		}
		return size;
	}
	
	public Directory Scanning(File F) {	
		directory.setSize(this.ScanningAll(directory, F));			//返回所有文件的size 给根目录
		directory.setName(F.getName());
		return directory;
	}

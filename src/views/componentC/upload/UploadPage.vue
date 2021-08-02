<template>
  <div>
    <el-form :model="uploadForm" onsubmit="return false">
      <el-form-item label="">
        <el-upload
          action=""
          :file-list="fileList"
          :before-upload="beforeUpload"
          :http-request="fnUploadRequest"
          :on-remove="removeFile"
          :on-preview="previewFile"
          accept=".doc,.docx,.ppt,.pptx,.xls,.xlsx,.pot,.txt,.zip"
          multiple
          ref="uploadForm"
        >
          <el-button size="small" type="primary" slot="trigger"
            >选取文件</el-button
          >
        </el-upload>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: "Upload",
  components: {},
  data() {
    return {
      fileList: [],
      uploadForm: {},
      file: {}, // 上传文件
    };
  },
  created() {
    this.init();
  },
  methods: {
    // 上传前的 文件名判断
    beforeUpload(file) {
      let testReg = file.name.substring(0, file.name.lastIndexOf("."));
      // console.log("testReg", testReg);
      let reg = /^(?!_)(?!.*?_$)[a-zA-Z0-9_\u4e00-\u9fa5]+$/;
      // console.log('res', reg.test(testReg));
      let bool = false;
      if (reg.test(testReg)) {
        bool = true;
      } else {
        this.$message({
          type: "error",
          message: "温馨提示：文件名仅支持：中文、英文、数字及下划线",
        });
        bool = false;
      }
      return bool;
    },
    // 上传
    fnUploadRequest(file, fileList) {
      console.log("上传文件的file", file);
      this.file = file.file;
      // 创建表单对象 用于数据的格式  + 用于添加流文件！
      let formData = new FormData();
      formData.append("files", this.file);
      let obj = {
        ...this.file,
        _t: Date.parse(new Date()) / 1000,
      };
      formData.append("_t", obj._t);
      formData.append("uid", this.file.uid);
			file.busiid = "111111";
			console.log("file", file,fileList);
			// 发起请求
      // axios
      //   .post(baseUrl + "/eap/uploadFile", formData, {
      //     headers: {
      //       From: "cmas-ui",
      //       "Content-Type": "multipart/form-data",
      //       Token: JSON.parse(sessionStorage.getItem("token")),
      //     },
      //   })
      //   .then(({ data }) => {
      //     console.log("上传文件data", data.dat);
      //     if (data.code == 0) {
      //       file.busiid = data.dat[0].busiid;
      //       this.uploadAllFile.push(data.dat[0]);
      //       this.$message({ type: "success", message: "上传文件成功" });
      //       file.name = data.dat[0].filename;
      //     } else {
      //       this.$message({ type: "error", message: data.dat });
      //     }
      //   });
    },
    // 上传文件的数据回显
    init() {
      // let uploadFile = [];
      // for (var index = 0; index < this.uploadFile.length; index++) {
      //   uploadFile.push({
      //     busiid: this.uploadFile[index].busiid,
      //     name: this.uploadFile[index].filename,
      //   });
      // }
      // console.log('回显uploadFile',uploadFile);
      // this.fileList = uploadFile;
    },
    // 删除文件
    removeFile(file) {
      console.log("删除的文件", file);
      // if (file.busiid) {
      //   removeFileGet(file.busiid).then(({ data }) => {
      //     if (data.code == 0) {
      //       this.$message({ type: "success", message: "删除文件成功" });
      //     } else {
      //       this.$message({ type: "error", message: data.dat });
      //     }
      //   });
      //   this.uploadAllFile = this.uploadAllFile.filter((item) => {
      //     return item.busiid != file.busiid;
      //   });
      // }
    },
    // 已经上传成功的 文件 可添加下载功能
    previewFile(file) {
      console.log("已经上传的 可以实现点击下载文件", file);
      //   let obj = {
      //     busiid: newV[i].busiid, // uid 需要使用
      //     filename: newV[i].filename,
      //   };
      //   requestDown({
      //       url: "/eap/downloadSingle",
      //       method: "get",
      //       responseType: "blob",
      //       params: {
      //         ...obj,
      //       },
      //     }).then((res) => {
      //       let link = document.createElement("a");
      //       let blob = new Blob([res]);
      //       link.style.display = "none";
      //       link.href = URL.createObjectURL(blob);
      //       if ("msSaveOrOpenBlob" in navigator) {
      //         window.navigator.msSaveOrOpenBlob(blob, obj.filename);
      //       } else {
      //         link.setAttribute("download", obj.filename);
      //         document.body.appendChild(link);
      //         link.click();
      //         document.body.removeChild(link);
      //       }
      //     });
    },
  },
};
</script>
<style  lang="scss" scoped>
::v-deep .el-button--small {
  padding: 6px 16px !important;
}
::v-deep .el-upload-list {
  position: relative;
  left: 100px;
  top: -34px;
  width: 640px;
  // background: #000;
  clear: both;
  li {
    float: left;
    width: 50% !important;
  }
  .el-upload-list__item {
    margin-top: 10px !important;
  }
}
::v-deep .el-upload--text {
  width: 100px;
  height: 50px;
}
</style>

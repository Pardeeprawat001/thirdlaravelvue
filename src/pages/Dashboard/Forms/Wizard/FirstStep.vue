<template>
  <div>
    <h5 class="info-text">
      Let's start with the basic information (with validation)
    </h5>
    <div class="row justify-content-center">
      <div class="col-sm-4">
        <div class="picture-container">
          <el-upload
            class="picture"
            action="https://jsonplaceholder.typicode.com/posts/"
            :on-change="handlePreview"
            :auto-upload="false"
            :show-file-list="false"
          >
            <img
              v-if="model.imageUrl"
              :src="model.imageUrl"
              class="picture-src"
            />
          </el-upload>
          <h6 class="description">Choose Picture</h6>
        </div>
      </div>
      <div class="col-sm-6">
        <fg-input
          class="form-control-lg"
          name="firstName"
          placeholder="First Name (required)"
          v-model="model.firstName"
          v-validate="modelValidations.firstName"
          :error="getError('firstName')"
          addon-left-icon="now-ui-icons users_circle-08"
        >
        </fg-input>

        <fg-input
          class="form-control-lg"
          name="lastName"
          placeholder="Last Name (required)"
          v-model="model.lastName"
          v-validate="modelValidations.lastName"
          :error="getError('lastName')"
          addon-left-icon="now-ui-icons text_caps-small"
        >
        </fg-input>
      </div>
      <div class="col-12 col-sm-10 mt-3">
        <fg-input
          class="form-control-lg"
          name="email"
          placeholder="Email (required)"
          v-model="model.email"
          v-validate="modelValidations.email"
          :error="getError('email')"
          addon-left-icon="now-ui-icons text_caps-small"
        >
        </fg-input>
      </div>
    </div>
  </div>
</template>
<script>
import { Upload } from "element-ui";

export default {
  components: {
    [Upload.name]: Upload,
  },
  data() {
    return {
      model: {
        firstName: "",
        lastName: "",
        email: "",
        imageUrl: "/img/default-avatar.png",
      },
      modelValidations: {
        firstName: {
          required: true,
          min: 5,
        },
        lastName: {
          required: true,
          min: 5,
        },
        email: {
          required: true,
          email: true,
        },
      },
    };
  },
  methods: {
    handlePreview(file) {
      this.model.imageUrl = URL.createObjectURL(file.raw);
    },
    getError(fieldName) {
      return this.errors.first(fieldName);
    },
    validate() {
      return this.$validator.validateAll().then((res) => {
        this.$emit("on-validated", res, this.model);
        return res;
      });
    },
  },
};
</script>
<style>
</style>

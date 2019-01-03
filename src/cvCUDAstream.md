```cpp
#include <fmt/printf.h>
#include <opencv2/opencv.hpp>

using namespace cv;

struct GPU_DATA {
  cuda::GpuMat d_color;
  std::vector<cuda::GpuMat> d_channels;
};

Mat blur_serial(const Mat &input_image, GPU_DATA &data) {
  data.d_color.upload(input_image);

  cuda::split(data.d_color, data.d_channels);

  const auto gaussian =
      cuda::createGaussianFilter(CV_8UC1, CV_8UC1, {11, 11}, 1.5);
  for (auto &cn : data.d_channels) {
    gaussian->apply(cn, cn);
  }

  cuda::merge(data.d_channels, data.d_color);

  Mat ret;
  data.d_color.download(ret);
  return ret;
}

Mat blur_parallel(const Mat &input_image, GPU_DATA &data) {
  data.d_color.upload(input_image);
  cuda::split(data.d_color, data.d_channels);

  std::vector<cuda::Stream> streams(3);
  const auto gaussian =
      cuda::createGaussianFilter(CV_8UC1, CV_8UC1, {11, 11}, 1.5);
  size_t i = 0;
  for (auto &cn : data.d_channels) {
    gaussian->apply(cn, cn, streams[i]);
    i++;
  }
  for (auto &stream : streams) {
    stream.waitForCompletion();
  }

  cuda::merge(data.d_channels, data.d_color);

  Mat ret;
  data.d_color.download(ret);
  return ret;
}

int main() {
  const Mat image =
      imread("/home/afterburner/Pictures/book.jpeg", IMREAD_COLOR);
  if (image.empty()) {
    fmt::print("image not found!\n");
    return 2;
  }
  auto count_start = getTickCount();
  GPU_DATA data;
  Mat image_out;
  for (int i = 0; i < 20; i++) {
    image_out = blur_serial(image, data);
  }
  fmt::print("Time elapsed per loop for serial: {}\n",
             (getTickCount() - count_start) / getTickFrequency() / 20.f);
  count_start = getTickCount();
  for (int i = 0; i < 20; i++) {
    image_out = blur_parallel(image, data);
  }
  fmt::print("Time elapsed per loop for parallel: {}\n",
             (getTickCount() - count_start) / getTickFrequency() / 20.f);
}

```
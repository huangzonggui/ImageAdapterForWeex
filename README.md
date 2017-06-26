# ImageAdapterForWeex
Simple weex image adapter.
weex 默认没有实现图片加载，这是我在网上找的最简单的图片加载实现了。。

```android
package pub.yanglong.novel.weex;

import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.os.AsyncTask;
import android.util.Log;
import android.widget.ImageView;

import com.taobao.weex.adapter.IWXImgLoaderAdapter;
import com.taobao.weex.common.WXImageStrategy;
import com.taobao.weex.dom.WXImageQuality;

import java.io.InputStream;
import java.net.URL;

/**
 * Created by YangLong on 2017/5/21.
 */

public class ImageAdapter implements IWXImgLoaderAdapter {
    @Override
    public void setImage(final String url, final ImageView view, WXImageQuality quality, WXImageStrategy strategy) {
        Log.d("hello", url);

        final Bitmap[] bmp = new Bitmap[1];

        new AsyncTask<Void, Void, Void>() {
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    InputStream in = new URL(url).openStream();
                    bmp[0] = BitmapFactory.decodeStream(in);
                } catch (Exception e) {
                    // log error
                }
                return null;
            }

            @Override
            protected void onPostExecute(Void result) {
                if (bmp[0] != null)
                    view.setImageBitmap(bmp[0]);
            }

        }.execute();
    }
}

```

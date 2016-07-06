sRGB
===================================

Use `EGL_GL_COLORSPACE_KHR, EGL_GL_COLORSPACE_SRGB_KHR` as attribute for `eglCreateWindowSurface` (not context) (`EGL_KHR_gl_colorspace` extension).

Could only find one (partial) example for Android :
* https://github.com/Samsung/GearVRf/blob/master/GVRf/Framework/framework/src/main/java/org/gearvrf/VrapiActivityHandler.java
* the idea is to use `GLSurfaceView.setEGLWindowSurfaceFactory` and pass the values in `createWindowSurface` to `eglCreateWindowSurface`

```java
public GLSurfaceView(Context context, AttributeSet attrs) {
    super(context, attrs);
    this.setEGLWindowSurfaceFactory(mWindow_sRGB_SurfaceFactory);
    this.setEGLConfigChooser(8, 8, 8, 8, 24, 8);
    this.setEGLContextClientVersion(2);
}

private static final String TAG = "GLSurfaceView";
private final EGLWindowSurfaceFactory mWindow_sRGB_SurfaceFactory = new EGLWindowSurfaceFactory() {

    public EGLSurface createWindowSurface(EGL10 egl, EGLDisplay display,
                                            EGLConfig config, Object nativeWindow) {
        EGLSurface result = null;
        final int EGL_GL_COLORSPACE_KHR = 0x309D;
        final int EGL_GL_COLORSPACE_SRGB_KHR = 0x3089;
        final int[] surfaceAttribs = {
                EGL_GL_COLORSPACE_KHR, EGL_GL_COLORSPACE_SRGB_KHR,
                EGL10.EGL_NONE
        };
        try {
            result = egl.eglCreateWindowSurface(display, config, nativeWindow, surfaceAttribs);
        } catch (IllegalArgumentException e) {
            // This exception indicates that the surface flinger surface
            // is not valid. This can happen if the surface flinger surface has
            // been torn down, but the application has not yet been
            // notified via SurfaceHolder.Callback.surfaceDestroyed.
            // In theory the application should be notified first,
            // but in practice sometimes it is not. See b/4588890
            Log.e(TAG, "eglCreateWindowSurface", e);
        }
        return result;
    }

    public void destroySurface(EGL10 egl, EGLDisplay display,
                                EGLSurface surface) {
        egl.eglDestroySurface(display, surface);
    }
};
```
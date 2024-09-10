# Hi there 👋

<!--
**nnspider/nnspider** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
                print('Error', error)

            try:
                if scale != 2:
                    interpolation = cv2.INTER_AREA if scale < 2 else cv2.INTER_LANCZOS4
                    h, w = img.shape[0:2]
                    output = cv2.resize(output, (int(w * scale / 2), int(h * scale / 2)), interpolation=interpolation)
            except Exception as error:
                print('wrong scale input.', error)

            if img_mode == 'RGBA':  # RGBA images should be saved in png format
                extension = 'png'
            # save_path = f'output/out.{extension}'
            # cv2.imwrite(save_path, output)
            out_path = Path(tempfile.mkdtemp()) / f'out.{extension}'
            cv2.imwrite(str(out_path), output)
        except Exception as error:
            print('global exception: ', error)
        finally:
            clean_folder('output')
        return out_path


def clean_folder(folder):
    for filename in os.listdir(folder):
        file_path = os.path.join(folder, filename)
        try:
            if os.path.isfile(file_path) or os.path.islink(file_path):
                os.unlink(file_path)
            elif os.path.isdir(file_path):
                shutil.rmtree(file_path)
        except Exception as e:
            print(f'Failed to delete {file_path}. 
